---
title: turtle example turtletest (snippet)
date: 2020-02-09
tags: ["python"]
---
Python turtle example 'turtletest'

Functions in program: 
* `def drawOne():`
* `def colors():`

Modules used in program: 
* `import random`

## python turtletest

Python turtle example: turtletest

```python
from turtle import *
import random

bgcolor ("light blue")

def colors():
	for n in range(20):
	    pensize(random.randint(1,30))
	    pencolor(0.4, 0.0, 0.0)
	    forward(10)
	    pencolor(1.0, 0.2, 0.2)
	    forward(10)
	   

def drawOne():
	for n in range(5):
		penup()
		goto(random.randint(-300, 300), random.randint(-300, 300))
		pendown()
		colors()
		right(75)

for n in range(20):
    drawOne()


```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com
