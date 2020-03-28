---
title: tkinter example button cb (snippet)
date: 2020-02-09
tags: ["python"]
---
Python tkinter example 'button cb'


Modules used in program: 
* `import pygubu`
* `import os`
* `import sys`

## python button cb

Python tkinter example: button cb

```python
import sys
import os
 
try:
    import tkinter as tk
    from tkinter import messagebox
except:
    import Tkinter as tk
    import tkMessageBox as messagebox
 
sys.path.append(os.path.join(os.path.dirname(__file__), '../'))
 
import pygubu
 
 
class Myapp:
    def __init__(self, master):
        self.builder = builder = pygubu.Builder()
        fpath = os.path.join(os.path.dirname(__file__),"button_cb.ui")
        builder.add_from_string(uinline)
        #builder.add_from_file(fpath)
 
        mainwindow = builder.get_object('mainwindow', master)
 
        builder.connect_callbacks(self)
 
        callbacks = {
            'on_button2_clicked': self.on_button2_clicked
            }
 
        builder.connect_callbacks(callbacks)
 
    def on_my_button_clicked(self):
        messagebox.showinfo('From callback', 'My button was clicked !!')
 
    def on_button2_clicked(self):
        messagebox.showinfo('From callback', 'Button 2 was clicked !!')

uinline = """<?xml version="1.0" ?>
<interface>
  <object class="ttk.Frame" id="mainwindow">
    <property name="height">250</property>
    <property name="padding">10</property>
    <property name="width">250</property>
    <layout>
      <property name="column">0</property>
      <property name="row">0</property>
      <rows>
        <row id="1">
          <property name="pad">10</property>
        </row>
        <row id="0">
          <property name="pad">10</property>
        </row>
      </rows>
    </layout>
    <child>
      <object class="ttk.Label" id="ttk.Label_1">
        <property name="anchor">e</property>
        <property name="text">Button command test ? ouch!!</property>
        <layout>
          <property name="column">0</property>
          <property name="sticky">ew</property>
          <property name="columnspan">1</property>
          <property name="row">0</property>
        </layout>
      </object>
    </child>
    <child>
      <object class="ttk.Button" id="my_button">
        <property name="command">on_my_button_clicked</property>
        <property name="text">Click me</property>
        <layout>
          <property name="column">0</property>
          <property name="row">1</property>
        </layout>
      </object>
    </child>
    <child>
      <object class="ttk.Button" id="ttk.Button_2">
        <property name="command">on_button2_clicked</property>
        <property name="text">Button 2</property>
        <layout>
          <property name="column">1</property>
          <property name="row">1</property>
        </layout>
      </object>
    </child>
  </object>
</interface>
"""

if __name__ == '__main__':
    root = tk.Tk()
    app = Myapp(root)
    root.mainloop()


```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com