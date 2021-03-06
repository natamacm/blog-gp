---
title: pygtk example ytclipr (snippet)
date: 2020-02-10
tags: ["python"]
---
Python pygtk example 'ytclipr'

Functions in program: 
* `def clip():`

Modules used in program: 
* `import pafy  # https://github.com/np1/pafy`
* `import notify2  # https://pypi.python.org/pypi/notify2`
* `import keybinder`
* `import gtk`
* `import pygtk`
* `import sys`

## python ytclipr

Python pygtk example: ytclipr

```python
# Python YouTube downloader
# 1. start script
# 2. copy youtube url into clipboard
# 3. press ctrl-d to start downloading

import sys

import pygtk
pygtk.require('2.0')
import gtk
import keybinder
import notify2  # https://pypi.python.org/pypi/notify2

sys.path.insert(0, '/srv/_platforms/pafy')
import pafy  # https://github.com/np1/pafy
# https://github.com/rg3/youtube-dl  Small command-line program to download videos from YouTube.com
# https://github.com/Zulko/moviepy  Python module for script-based movie editing


def clip():
    summary = 'ClipClip'
    text = gtk.clipboard_get().wait_for_text().strip()
    engaged = False
    if '//www.youtube.com/' in text:
        engaged = True
        video = pafy.new(text)
        best = video.getbest(preftype="mp4")
        summary += ' video engaged (%s)' % video.length
        text += '\n%s\n%s' % (video.title, best)
        print('engaged:', text)

    notify2.Notification(summary, text).show()

    if engaged:
        myfilename = "/home/stav/Videos/clpclp/" + best.title + "." + best.extension
        best.download(filepath=myfilename)

    #gtk.main_quit()

if __name__ == '__main__':
    notify2.init("ClipClip")
    keybinder.bind("<Ctrl>D", clip)
    gtk.main()


```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com
