---
title: tkinter example dynamic label (snippet)
date: 2020-02-09
tags: ["python"]
---
Python tkinter example 'dynamic label'

Functions in program: 
* `def update_status():`

Modules used in program: 
* `import tkinter as tk`

## python dynamic label

Python tkinter example: dynamic label

```python
#AIDES: https://stackoverflow.com/questions/18047636/python-is-it-possible-to-create-an-tkinter-label-which-has-a-dynamic-string-whe

import tkinter as tk

root = tk.Tk()

status = tk.Label(root, text="Working")
status.grid()

def update_status():

    # Get the current message
    current_status = status["text"]

    # If the message is "Working...", start over with "Working"
    if current_status.endswith("..."): current_status = "Working"

    # If not, then just add a "." on the end
    else: current_status += "."

    # Update the message
    status["text"] = current_status

    # After 1 second, update the status
    root.after(1000, update_status)

# Launch the status message after 1 millisecond (when the window is loaded)
root.after(1, update_status)

root.mainloop()

```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com
