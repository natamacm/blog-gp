---
title: pygtk example socket (snippet)
date: 2020-02-10
tags: ["python"]
---
Python pygtk example 'socket'

Functions in program: 
* `def plugged_event(widget):`

Modules used in program: 
* `import gtk,sys`
* `import pygtk`
* `import string`

## python socket

Python pygtk example: socket

```python
#!/usr/bin/python

import string

import pygtk
pygtk.require('2.0')
import gtk,sys

window = gtk.Window()
window.show()

socket = gtk.Socket()
socket.show()
window.add(socket)

print("Socket ID=", socket.get_id())
window.connect("destroy", lambda w: gtk.main_quit())

def plugged_event(widget):
    print("I (", widget, ") have just had a plug inserted!")

socket.connect("plug-added", plugged_event)

if len(sys.argv) == 2:
    socket.add_id(long(sys.argv[1]))

gtk.main()

```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com
