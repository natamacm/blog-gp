---
title: turtle example tc paint (snippet)
date: 2020-02-09
tags: ["python"]
---
Python turtle example 'tc paint'

Functions in program: 
* `def 主函數():`
* `def 改變顏色(x=0, y=0):`
* `def 切換上下(x=0, y=0):`

## python tc paint

Python turtle example: tc paint

```python
#!/usr/bin/env python3
'''龜例如套房：

            tdemo_paint.py

一個簡單的事件驅動的畫圖程序

 - 鼠標左鍵移動龜
 - 鼠標中鍵的顏色變化
 - 鼠標右鍵toogles betweem筆了
（沒有引出的烏龜移動時）和
下筆（行繪製） 。如果筆了如下
至少兩個落筆移動時，多邊形是
包括起點被充滿。
 -------------------------------------------
 點擊進入畫布玩
 使用三個鼠標鍵。
 -------------------------------------------
          要退出，請按STOP按鈕
 -------------------------------------------=== 以上由 Google 翻譯，請協助改善 ===
'''
from turtle_tc import *

def 切換上下(x=0, y=0):
    if 筆()["pendown"]:
        結束填()
        提筆()
    else:
        下筆()
        開始填()

def 改變顏色(x=0, y=0):
    global 顏色們
    顏色們 = 顏色們[1:]+顏色們[:1]
    顏色(顏色們[0])

def 主函數():
    global 顏色們
    形狀("circle")
    重設大小模式("user")
    形狀大小(.5)
    筆寬(3)
    顏色們=[紅, 綠, 藍, 黃]
    顏色(顏色們[0])
    切換上下()
    在點擊幕時(前往,1)
    在點擊幕時(改變顏色,2)
    在點擊幕時(切換上下,3)
    return "EVENTLOOP"

if __name__ == "__main__":
    訊息 = 主函數()
    印(訊息)
    主迴圈()

# Above: "tc_paint.py", by Renyuan Lyu (呂仁園), 2015-01-27
# Original: "paint.py", by Gregor Lingl. 


```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com
