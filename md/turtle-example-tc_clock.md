---
title: turtle example tc clock (snippet)
date: 2020-02-09
tags: ["python"]
---
Python turtle example 'tc clock'

Functions in program: 
* `def 主函數():`
* `def 滴答():`
* `def 年月日期(z):`
* `def 星期標籤(t):`
* `def 設立():`
* `def 鐘面(半徑):`
* `def 作指針形狀(名, 長度, 尺寸大小):`
* `def 指針(長度, 尺寸大小):`
* `def 跳(距離, 角度=0):`

## python tc clock

Python turtle example: tc clock

```python
#!/usr/bin/env python3
#  - * - 編碼： CP1252 - * - 
'''龜例如套房：

             tdemo_clock.py

增強的時鐘程序，顯示日期
和時間
  ------------------------------------
   按STOP退出程序！
  ------------------------------------=== 以上由 Google 翻譯，請協助改善 ===
'''
from turtle_tc import *
from datetime import datetime

def 跳(距離, 角度=0):
    提筆()
    右轉(角度)
    前進(距離)
    左轉(角度)
    下筆()

def 指針(長度, 尺寸大小):
    前進(長度*1.15)
    右轉(90)
    前進(尺寸大小/2.0)
    左轉(120)
    前進(尺寸大小)
    左轉(120)
    前進(尺寸大小)
    左轉(120)
    前進(尺寸大小/2.0)

def 作指針形狀(名, 長度, 尺寸大小):
    重設()
    跳(-長度*0.15)
    開始多邊形()
    指針(長度, 尺寸大小)
    結束多邊形()
    指針形式 = 取多邊形()
    登記形狀(名, 指針形式)

def 鐘面(半徑):
    重設()
    筆粗(7)
    for i in 範圍(60):
        跳(半徑)
        if i % 5 == 0:
            前進(25)
            跳(-半徑-25)
        else:
            點(3)
            跳(-半徑)
        右轉(6)

def 設立():
    global 秒針, 分針, 時針, 寫手
    模式(角度從北開始順時針)
    作指針形狀("秒針", 125, 25)
    作指針形狀("分針",  130, 25)
    作指針形狀("時針", 90, 25)
    鐘面(160)
    秒針 = 龜類()
    秒針.形狀("秒針")
    秒針.顏色("gray20", "gray80")
    分針 = 龜類()
    分針.形狀("分針")
    分針.顏色("blue1", "red1")
    時針 = 龜類()
    時針.形狀("時針")
    時針.顏色("blue3", "red3")
    for 指針 in 秒針, 分針, 時針:
        指針.重設大小模式("user")
        指針.形狀大小(1, 1, 3)
        指針.速度(0)
    藏龜()
    寫手 = 龜類()
    # writer.mode （ “標誌” ）
    寫手.藏龜()
    寫手.提筆()
    寫手.後退(85)

def 星期標籤(t):
    星期標籤 = ["拜一", "拜二", "拜三",
        "拜四", "拜五", "拜六", "拜日"]
    return 星期標籤[t.weekday()]

def 年月日期(z):
    monat = ["一月", "二月", "三月", "四月", "五月", "六月",
             "七月", "八月", "九月", "十月", "十一月", "十二月"]
    j = z.year
    m = monat[z.month - 1]
    t = z.day
    return "%s %d %d" % (m, t, j)

def 滴答():
    t = datetime.today()
    秒數 = t.second + t.microsecond*0.000001
    minute = t.minute + 秒數/60.0
    時數 = t.hour + minute/60.0
    try:
        追蹤(假)  # 終結者可以發生在這裡
        寫手.清除()
        寫手.回家()
        寫手.前進(65)
        寫手.寫(星期標籤(t),
                     align="center", font=("Courier", 14, "bold"))
        寫手.後退(150)
        寫手.寫(年月日期(t),
                     align="center", font=("Courier", 14, "bold"))
        寫手.前進(85)
        追蹤(真)
        秒針.設頭向(6*秒數)  # 或點擊這裡
        分針.設頭向(6*minute)
        時針.設頭向(30*時數)
        追蹤(真)
        在計時後(滴答, 100)
    except Terminator:
        pass  # turtledemo用戶按STOP

def 主函數():
    追蹤(假)
    設立()
    追蹤(真)
    滴答()
    return "EVENTLOOP"

if __name__ == "__main__":
    模式(角度從北開始順時針)
    訊息 = 主函數()
    印(訊息)
    主迴圈()

# Above: "tc_clock.py", by Renyuan Lyu (呂仁園), 2015-01-27
# Original: "clock.py", by Gregor Lingl. 


```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com
