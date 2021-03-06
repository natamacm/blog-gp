---
title: pil example fsblog-20170302-transform images (snippet)
date: 2020-03-02
tags: ["python"]
---
Python pil example 'fsblog-20170302-transform images'

Functions in program: 
* `def original_colors(original, stylized):`

Modules used in program: 
* `import time`
* `import zmq_utils`
* `import zmq`
* `import chainer`
* `import time`
* `import argparse`
* `import numpy as np`

## python fsblog-20170302-transform images

Python pil example: fsblog-20170302-transform images

```python
from __future__ import print_function
import numpy as np
import argparse
from PIL import Image, ImageFilter
import time

import chainer
from chainer import cuda, Variable, serializers
from net import *

import zmq
import zmq_utils
import time


parser = argparse.ArgumentParser(description='Real-time style transfer image generator')
parser.add_argument('--gpu', '-g', default=-1, type=int,
                    help='GPU ID (negative value indicates CPU)')
parser.add_argument('--model', '-m', default='models/style.model', type=str)
parser.add_argument('--out', '-o', default='out.jpg', type=str)
parser.add_argument('--median_filter', default=3, type=int)
parser.add_argument('--padding', default=50, type=int)
parser.add_argument('--keep_colors', action='store_true')
parser.set_defaults(keep_colors=False)
args = parser.parse_args()

# from 6o6o's fork. https://github.com/6o6o/chainer-fast-neuralstyle/blob/master/generate.py
def original_colors(original, stylized):
    h, s, v = original.convert('HSV').split()
    hs, ss, vs = stylized.convert('HSV').split()
    return Image.merge('HSV', (h, s, vs)).convert('RGB')

model = FastStyleNet()
serializers.load_npz(args.model, model)
if args.gpu >= 0:
    cuda.get_device(args.gpu).use()
    model.to_gpu()
xp = np if args.gpu < 0 else cuda.cupy

print("The model has been read")



# Setup ZeroMQ image publisher & receiver
context = zmq.Context()
sub = context.socket(zmq.SUB)
sub.setsockopt_string(zmq.SUBSCRIBE, "image")
sub.set_hwm(1)
sub.connect("tcp://<ラズパイ３のIPアドレス>:5558")

pub = context.socket(zmq.PUB)
pub.set_hwm(1)
pub.connect("tcp://<ラズパイ３のIPアドレス>:5559")

print("Starting...")

last = time.time()

while True:

    # Convert cv::Mat to PIL.Image
    original = zmq_utils.recv_image(sub)
    original = Image.fromarray(original)
    b,g,r = original.split()
    original = Image.merge("RGB",(r,g,b))

    image = np.asarray(original, dtype=np.float32).transpose(2, 0, 1)
    image = image.reshape((1,) + image.shape)

    if args.padding > 0:
        image = np.pad(image, [[0, 0], [0, 0], [args.padding, args.padding], [args.padding, args.padding]], 'symmetric')
        image = xp.asarray(image)

    x = Variable(image)

    y = model(x)

    result = cuda.to_cpu(y.data)

    print("result obtained")

    # Free the memory
    y.unchain_backward()

    if args.padding > 0:
        result = result[:, :, args.padding:-args.padding, args.padding:-args.padding]

    result = np.uint8(result[0].transpose((1, 2, 0)))
    med = Image.fromarray(result)

    if args.median_filter > 0:
        med = med.filter(ImageFilter.MedianFilter(args.median_filter))
    if args.keep_colors:
        med = original_colors(original, med)

    tick = time.time()
    print(tick - last, 'sec')
    last = tick

    #med.save(args.out)

    # Convert PIL.Image back to cv::Mat
    r,g,b = med.split()
    med = Image.merge("RGB",(b,g,r))
    med4pub = np.asarray(med)
    zmq_utils.send_image(pub, med4pub)

```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com
