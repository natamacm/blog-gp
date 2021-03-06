---
title: pil example tar reader pytorch (snippet)
date: 2020-03-02
tags: ["python"]
---
Python pil example 'tar reader pytorch'


Modules used in program: 
* `import torch`
* `import pandas as pd`
* `import os`
* `import io`
* `import tarfile`
* `import random`
* `import numpy as np`

## python tar reader pytorch

Python pil example: tar reader pytorch

```python
"""
# Mohammad Doosti Lakhani - 2019

Hi,
This works if you have image dataset in `.tar` file.
You have to have a `.csv` or `.txt` file, including a name per line of your dataset.
"""


from PIL import Image
from torchvision.transforms import ToTensor, ToPILImage
import numpy as np
import random

import tarfile
import io
import os
import pandas as pd

from torch.utils.data import Dataset
import torch

class YourDataset(Dataset):
    def __init__(self, txt_path='filelist.txt', img_dir='data.tar', transform=None):
        """
        Initialize data set as a list of IDs corresponding to each item of data set

        :param img_dir: path to image files as a uncompressed tar archive
        :param txt_path: a text file containing names of all of images line by line
        :param transform: apply some transforms like cropping, rotating, etc on input image
        """

        df = pd.read_csv(txt_path, sep=' ', index_col=0)
        self.img_names = df.index.values
        self.txt_path = txt_path
        self.img_dir = img_dir
        self.transform = transform
        self.to_tensor = ToTensor()
        self.to_pil = ToPILImage()
        self.tf = tarfile.open(self.img_dir)

    def get_image_from_tar(self, name):
        """
        Gets a image by a name gathered from file list csv file

        :param name: name of targeted image
        :return: a PIL image
        """
        image = self.tf.extractfile(name)
        image = image.read()
        image = Image.open(io.BytesIO(image))
        return image

    def __len__(self):
        """
        Return the length of data set using list of IDs

        :return: number of samples in data set
        """
        return len(self.img_names)

    def __getitem__(self, index):
        """
        Generate one item of data set.

        :param index: index of item in IDs list

        :return: a sample of data as a dict
        """

        if index == (self.__len__() - 1) :  # close tarfile opened in __init__
            self.tf.close()

        
        image = self.get_image_from_tar(self.img_names[index])
       
        if self.transform is not None:
            image = self.transform(image)

        sample = {'X': image}

        return sample


```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com
