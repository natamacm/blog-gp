---
title: PIL example LoadImageFromWeb (snippet)
date: 2020-03-02
tags: ["python"]
---
Python PIL example 'LoadImageFromWeb'


Modules used in program: 
* `import numpy as np`
* `import urllib2`

## python LoadImageFromWeb

Python PIL example: LoadImageFromWeb

```python
from PIL import Image as pil
import urllib2
import numpy as np
source = "http://something"

req = urllib2.Request(source, headers={'User-Agent' : "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/536.5 (KHTML, like Gecko) Chrome/19.0.1084.54 Safari/536.5"})
img_file = urllib2.urlopen(req)
im = StringIO(img_file.read()) # You can skip this and directly convert to numpy arrays
source = pil.open(im).convert("RGB")
_pilImage = source
npimg = np.fromstring(_pilImage.tostring(), dtype=np.uint8)
npimg = cv2.cvtColor(npimg, cv2.cv.CV_RGB2BGR)

```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com