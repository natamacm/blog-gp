---
title: pil example FacialRecon (snippet)
date: 2020-03-02
tags: ["python"]
---
Python pil example 'FacialRecon'


Modules used in program: 
* `import face_recognition`
* `import pickle`
* `import glob, os, codecs, json, imutils, cv2`
* `import numpy as np`

## python FacialRecon

Python pil example: FacialRecon

```python
from PIL import Image, ImageDraw
from imutils.video import FileVideoStream
from imutils.video import VideoStream
import numpy as np
import glob, os, codecs, json, imutils, cv2
import pickle
import face_recognition

from libs.models import FrameModel
from .models.FaceBundle import FaceBundle


class FaceRecognition:
    def __init__(self, storageFolderPath='./storage/',
                 knownFolderPath='./known/',
                 unkwonFolderPath='./unknown/',
                 outputFolderPath='./output',
                 outputData='outputData.json',
                 tolerance=0.6):

        self.storageFolderPath = storageFolderPath
        self.knownFolderPath = knownFolderPath
        self.unkwonFolderPath = unkwonFolderPath
        self.outputFolderPath = outputFolderPath

        self.faceBundleFile = storageFolderPath + 'facebundlefile.obj'
        self.csvFile = outputData
        self.toleranceRate = tolerance
        self.knownFaces = []

        if os.path.exists(self.faceBundleFile):
            face_file = open(self.faceBundleFile, 'rb')
            self.knownFaces = pickle.load(face_file)
            face_file.close()

    #
    #   Generic
    #
    def setKnownFolderPath(self, knownFolderPath):
        self.knownFolderPath = knownFolderPath

    def setUnknownFolderPath(self, unkwonFolderPath):
        self.unkwonFolderPath = unkwonFolderPath

    def setOuputFolderPath(self, outputFolderPath):
        self.outputFolderPath = outputFolderPath

    def setOuputData(self, outputData):
        self.outputData = outputData

    #
    #   Private Functions
    #

    #
    #   Dada uma imagem, Retorna uma lista com todas as Faces presentes
    #
    def __parseFaces(self, filePath, image_read=None) -> list:
        listFaces: list = []
        # Load test image to find faces in
        if image_read is None:
            image_read = face_recognition.load_image_file(filePath)

        # File Identification
        filename_w_ext = os.path.basename(filePath)
        filename, file_extension = os.path.splitext(filename_w_ext)

        # Find faces in test image
        # print(("image read:" + image_read))
        face_locations = face_recognition.face_locations(image_read)
        face_encodings = face_recognition.face_encodings(image_read, face_locations)
        face_landmarks = face_recognition.face_landmarks(image_read)

        count = 0
        for location, encodings, landmarks in zip(face_locations, face_encodings, face_landmarks):
            faceBundle = FaceBundle(filename, file_extension, count)
            faceBundle.setLocation(location)
            faceBundle.setEncodings(encodings)
            faceBundle.setLandmarks(landmarks)
            listFaces.append(faceBundle)
            count += 1
        return listFaces

    def __hasMatch(self, knownEncodings, faceBundle, debug=True):
        matches = face_recognition.compare_faces(knownEncodings, faceBundle.getEncodings(),
                                                 tolerance=self.toleranceRate)
        if debug:
            for i in range(0, len(self.knownFaces)):
                if True == matches[i]:
                    print(faceBundle.getName(), '==', self.knownFaces[i].getName())
        return matches

    def __drawImage(self, drawInstance, faceBundle, label, drawBox=True, drawLandmarks=True, drawLabel=True):
        top, right, bottom, left = faceBundle.getLocation()

        # Draw box
        if drawBox:
            drawInstance.rectangle(((left, top), (right, bottom)), outline=(255, 255, 0))

        # Draw Landmarks
        if drawLandmarks:
            for __, value in faceBundle.getLandmarks().items():
                drawInstance.line(value, fill=(27, 189, 230), width=1)

        # Draw label
        if drawLabel:
            text_width, text_height = drawInstance.textsize(label)
            drawInstance.rectangle(((left, bottom - text_height - 10), (right, bottom)), fill=(255, 255, 0),
                                   outline=(255, 255, 0))
            drawInstance.text((left + 6, bottom - text_height - 5), label, fill=(0, 0, 0))

    #
    #   Public Functions
    #

    #
    #   Recorta todas as Faces de uma Imagem e as Salva
    #
    def pullFaces(self, imagePath, outputExtension='jpg'):
        listFaces = self.__parseFaces(imagePath)
        image = face_recognition.load_image_file(imagePath)
        for face in listFaces:
            top, right, bottom, left = face.getLocation()
            face_image = image[top:bottom, left:right]
            pil_image = Image.fromarray(face_image)
            resultPath = "{}/{}.jpg".format(self.outputFolderPath, face.getName())
            pil_image.save(resultPath)
        print("pullFaces -- {} Faces Found".format(len(listFaces)))
        print("pullFaces -- Done")

        return listFaces

    #
    # Known Faces
    #
    def parseKnownFaces(self, image_extension=''):
        if not self.knownFaces:
            files_regex = self.knownFolderPath + '*' + image_extension
            files = glob.glob(files_regex)
            for filename in files:
                faceBundleList = self.__parseFaces(filename)
                if len(faceBundleList) != 0:
                    self.knownFaces.append(faceBundleList[0])
                else:
                    print("Encoding Error on", filename)
            self.saveKnownFaces()

    def addKnownFace(self, filePath):
        faceBundleList = self.__parseFaces(filePath)
        if len(faceBundleList):
            self.knownFaces.append(faceBundleList[0])
            self.saveKnownFaces()

        return faceBundleList[0].toData()

    def findMatches(self, filePath, image_read=None, draw_matches=True, id='') -> list:
        faceList: list = []

        #   Find Faces
        faceBundleList = self.__parseFaces(filePath, image_read)

        #   Prepare to Draw
        if draw_matches:
            if image_read is None:
                image_read = face_recognition.load_image_file(filePath)
            pil_image = Image.fromarray(image_read)
            draw = ImageDraw.Draw(pil_image)

        #   Prepare to Match
        knownFacesEncoding = []
        for knownFace in self.knownFaces:
            knownFacesEncoding.append(knownFace.getEncodings())

        for faceBundle in faceBundleList:
            matches = self.__hasMatch(knownFacesEncoding, faceBundle)
            if draw_matches and len(matches) > 0 and True in matches:
                first_match_index = matches.index(True)
                name = self.knownFaces[first_match_index].getName()
                self.__drawImage(draw, faceBundle, name, drawBox=True)
                pil_image.save('{}/result_{}.jpg'.format(self.outputFolderPath, id))
            faceList.append(faceBundle.toData())
        return faceList

    def videoRecognition(self, videoPath, fileStream=True, skipFrames=10, showVideo=False, id='') -> list:
        actual_frame: FrameModel
        frame_list: list = []
        # start the video stream thread
        print("[INFO] starting video stream thread...")

        # to stream from a file
        if fileStream:
            vs = FileVideoStream(videoPath).start()
        else:
            vs = VideoStream(src=0).start()

        frameCount = 0
        vs.thread.setName('Stream Thread')

        # loop over frames from the video stream
        while True:
            # if this is a file video stream, then we need to check if
            # there any more frames left in the buffer to process
            if fileStream and not vs.more() or vs.stopped:
                break

            # grab the frame from the threaded video file stream, resize
            # it, and convert it to grayscale channels
            frame = vs.read()
            frame = imutils.resize(frame, width=450)
            frameCount += 1

            # Recognition
            if frameCount % skipFrames == 0:
                print('At Frame #{}'.format(frameCount))
                face_list = self.findMatches(videoPath, image_read=frame, id='{}_{}'.format(id, frameCount))
                actual_frame = FrameModel.FrameModel(videoPath, frameCount)
                actual_frame.set_face_list(face_list)
                frame_list.append(actual_frame)

            # show the frame
            if showVideo:
                cv2.imshow("Frame", frame)
                key = cv2.waitKey(1) & 0xFF
                # if the `q` key was pressed, break from the loop
                if key == ord("q"):
                    break

        # do a bit of cleanup
        if showVideo:
            cv2.destroyAllWindows()
        vs.stop()

        return frame_list

    def saveKnownFaces(self):
        # dataArray = []
        # for faceBundle in self.knownFaces:
        #     jsonData = faceBundle.toData()
        #     dataArray.append(jsonData)
        # json.dump(dataArray, codecs.open(self.csvFile, 'a', encoding='utf-8'), separators=(',', ':'), sort_keys=True)
        try:
            face_bundle_file = open(self.faceBundleFile, 'wb')
            pickle.dump(self.knownFaces, face_bundle_file)
            face_bundle_file.close()
        except FileNotFoundError:
            print('File {} not Found'.format(self.faceBundleFile))

    def parseFromJson(self, json_path):
        obj_text = codecs.open(json_path, 'r', encoding='utf-8').read()
        b_new = json.loads(obj_text)
        print()
        # a_new = np.array(b_new)
    # def __writeData(self, data):
    #     with open(self.csvFile, 'a') as csvFile:
    #         writer = csv.writer(csvFile)
    #         writer.writerow(data)
    #     csvFile.close()

```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com
