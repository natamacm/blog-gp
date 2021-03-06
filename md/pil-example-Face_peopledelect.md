---
title: pil example Face peopledelect (snippet)
date: 2020-03-02
tags: ["python"]
---
Python pil example 'Face peopledelect'


Modules used in program: 
* `import cv2`
* `import imutils`
* `import argparse`
* `import numpy as np`

## python Face peopledelect

Python pil example: Face peopledelect

```python
 # import the necessary packages
from __future__ import print_function
from imutils.object_detection import non_max_suppression
from imutils import paths
import numpy as np
import argparse
import imutils
import cv2

# construct the argument parse and parse the arguments
ap = argparse.ArgumentParser()
ap.add_argument("-i", "--images", required=True, help="path to images directory")
args = vars(ap.parse_args())
# initialize the HOG descriptor/person   detector
hog = cv2.HOGDescriptor()
hog.setSVMDetector(cv2.HOGDescriptor_getDefaultPeopleDetector())
for imagePath in paths.list_images(args["images"]):
    framelist=[]
    # load the image and resize it to (1) reduce detection time
    # and (2) improve detection accuracy
    image = cv2.imread(imagePath)
    #image = imutils.resize(image, width=min(400, image.shape[1]))
    orig = image.copy()

    # detect people in the image
    (rects, weights) = hog.detectMultiScale(image, winStride=(4, 4),
        padding=(8, 8), scale=1.05)

     # draw the original bounding boxes
    for (x, y, w, h) in rects:
         cv2.rectangle(orig, (x, y), (x + w, y + h), (0, 0, 255), 2)
    rects = np.array([[x, y, x + w, y + h] for (x, y, w, h) in rects])
    pick = non_max_suppression(rects, probs=None, overlapThresh=0.65)

    for (xA, yA, xB, yB) in pick:
        cv2.rectangle(image, (xA, yA), (xB, yB), (0, 255, 0), 2)
        framelist.append((xA, yA, xB, yB))
    print(framelist)
     # show some information on the number of bounding boxes
    filename = imagePath[imagePath.rfind("/") + 1:]
    print("[INFO] {}: {} original boxes, {} after suppression".format(
          filename, len(rects), len(pick)))

    #cv2.imwrite('change.jpg', image, [int(cv2.IMWRITE_JPEG_QUALITY), 95])  # 默认95
    # cv2.imshow("Before NMS", orig)
    # cv2.imshow("After NMS", image)
    # cv2.waitKey(0)

```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com
