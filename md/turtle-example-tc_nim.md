---
title: turtle example tc nim (snippet)
date: 2020-02-09
tags: ["python"]
---
Python turtle example 'tc nim'

Functions in program: 
* `def 主函數():`
* `def 隨機移動(狀態):`
* `def 電腦揀棒子(狀態):`
* `def 隨機列():`

Modules used in program: 
* `import time`
* `import random`
* `import turtle_tc as turtle; from turtle_tc import *`

## python tc nim

Python turtle example: tc nim

```python
'''龜例如套房：

            tdemo_nim.py

玩NIM對計算機。播放器
誰需要最後一棒是贏家。

實現了模型 - 視圖 - 控制器
設計模式。=== 以上由 Google 翻譯，請協助改善 ===
'''


import turtle_tc as turtle; from turtle_tc import *
import random
import time

幕寬常數 = 640
幕高常數 = 480

最小棒子數常數 = 7
最大棒子數常數 = 31

垂直單位常數 = 幕高常數 // 12
水平單位常數 = 幕寬常數 // ((最大棒子數常數 // 5) * 11 + (最大棒子數常數 % 5) * 2)

S顏色常數 = (63, 63, 31)
H顏色常數 = (255, 204, 204)
顏色常數 = (204, 204, 255)

def 隨機列():
    return random.randint(最小棒子數常數, 最大棒子數常數)

def 電腦揀棒子(狀態):
    互斥或 = 狀態[0] ^ 狀態[1] ^ 狀態[2]
    if 互斥或 == 0:
        return 隨機移動(狀態)
    for z in 範圍(3):
        s = 狀態[z] ^ 互斥或
        if s <= 狀態[z]:
            移動 = (z, s)
            return 移動

def 隨機移動(狀態):
    m = max(狀態)
    while 真:
        z = random.randint(0,2)
        if 狀態[z] > (m > 1):
            break
    rand = random.randint(m > 1, 狀態[z]-1)
    return z, rand


class 捻遊戲模型類(object):
    def __init__(我, 遊戲):
        我.遊戲 = 遊戲

    def 設立(我):
        if 我.遊戲.狀態 not in [捻遊戲類.被創造狀態, 捻遊戲類.遊戲結束狀態]:
            return
        我.棒子們 = [隨機列(), 隨機列(), 隨機列()]
        我.玩家 = 0
        我.贏家 = 無
        我.遊戲.視圖.設立()
        我.遊戲.狀態 = 捻遊戲類.正在跑狀態

    def 移動(我, 列, 行):
        最大分裂數 = 我.棒子們[列]
        我.棒子們[列] = 行
        我.遊戲.視圖.通知移動(列, 行, 最大分裂數, 我.玩家)
        if 我.遊戲結束():
            我.遊戲.狀態 = 捻遊戲類.遊戲結束狀態
            我.贏家 = 我.玩家
            我.遊戲.視圖.通知結束()
        elif 我.玩家 == 0:
            我.玩家 = 1
            列, 行 = 電腦揀棒子(我.棒子們)
            我.移動(列, 行)
            我.玩家 = 0

    def 遊戲結束(我):
        return 我.棒子們 == [0, 0, 0]

    def 通知移動(我, 列, 行):
        if 我.棒子們[列] <= 行:
            return
        我.移動(列, 行)


class 棒子類(turtle.龜類):
    def __init__(我, 列, 行, 遊戲):
        turtle.龜類.__init__(我, visible=假)
        我.列 = 列
        我.行 = 行
        我.遊戲 = 遊戲
        x, y = 我.座標們(列, 行)
        我.形狀(方形)
        我.形狀大小(垂直單位常數/10.0, 水平單位常數/20.0)
        我.速度(0)
        我.提筆()
        我.前往(x,y)
        我.顏色(白)
        我.顯龜()

    def 座標們(我, 列, 行):
        包裹, 餘數 = divmod(行, 5)
        x = (3 + 11 * 包裹 + 2 * 餘數) * 水平單位常數
        y = (2 + 3 * 列) * 垂直單位常數
        return x - 幕寬常數 // 2 + 水平單位常數 // 2, 幕高常數 // 2 - y - 垂直單位常數 // 2

    def 令移動(我, x, y):
        if 我.遊戲.狀態 != 捻遊戲類.正在跑狀態:
            return
        我.遊戲.控制者.通知移動(我.列, 我.行)


class 捻遊戲視圖類(object):
    def __init__(我, 遊戲):
        我.遊戲 = 遊戲
        我.幕 = 遊戲.幕
        我.模型 = 遊戲.模型
        我.幕.色模式(255)
        我.幕.追蹤(假)
        我.幕.背景色((240, 240, 255))
        我.寫手 = turtle.龜類(visible=假)
        我.寫手.提筆()
        我.寫手.速度(0)
        我.棒子們 = {}
        for 列 in 範圍(3):
            for 行 in 範圍(最大棒子數常數):
                我.棒子們[(列, 行)] = 棒子類(列, 行, 遊戲)
        我.display("... a moment please ...")
        我.幕.追蹤(真)

    def display(我, 訊息1, 訊息2=無):
        我.幕.追蹤(假)
        我.寫手.清除()
        if 訊息2 is not 無:
            我.寫手.前往(0, - 幕高常數 // 2 + 48)
            我.寫手.筆色(紅)
            我.寫手.寫(訊息2, align="center", font=("Courier",18,"bold"))
        我.寫手.前往(0, - 幕高常數 // 2 + 20)
        我.寫手.筆色(黑)
        我.寫手.寫(訊息1, align="center", font=("Courier",14,"bold"))
        我.幕.追蹤(真)

    def 設立(我):
        我.幕.追蹤(假)
        for 列 in 範圍(3):
            for 行 in 範圍(我.模型.棒子們[列]):
                我.棒子們[(列, 行)].顏色(S顏色常數)
        for 列 in 範圍(3):
            for 行 in 範圍(我.模型.棒子們[列], 最大棒子數常數):
                我.棒子們[(列, 行)].顏色(白)
        我.display("輪到你！點擊一根棒子來移走它及其右邊的棒子")
        我.幕.追蹤(真)

    def 通知移動(我, 列, 行, 最大分裂數, 玩家):
        if 玩家 == 0:
            色彩 = H顏色常數
            for s in 範圍(行, 最大分裂數):
                我.棒子們[(列, s)].顏色(色彩)
        else:
            我.display(" ... thinking ...         ")
            time.sleep(0.5)
            我.display(" ... thinking ... aaah ...")
            色彩 = 顏色常數
            for s in 範圍(最大分裂數-1, 行-1, -1):
                time.sleep(0.2)
                我.棒子們[(列, s)].顏色(色彩)
            我.display("輪到你！點擊一根棒子來移走它及其右邊的棒子")

    def 通知結束(我):
        if 我.遊戲.模型.贏家 == 0:
            訊息2 = "恭喜，你贏了！"
        else:
            訊息2 = "歹勢，電腦贏了！"
        我.display("To play again press space bar. To leave press ESC.", 訊息2)

    def 清除(我):
        if 我.遊戲.狀態 == 捻遊戲類.遊戲結束狀態:
            我.幕.清除()


class 捻遊戲控制者類(object):

    def __init__(我, 遊戲):
        我.遊戲 = 遊戲
        我.棒子們 = 遊戲.視圖.棒子們
        我.繁忙狀態 = 假
        for 棒子 in 我.棒子們.values():
            棒子.在點擊時(棒子.令移動)
        我.遊戲.幕.在按鍵時(我.遊戲.模型.設立, 空白鍵)
        我.遊戲.幕.在按鍵時(我.遊戲.視圖.清除, 脫離鍵)
        我.遊戲.視圖.display("Press space bar to start game")
        我.遊戲.幕.聽()

    def 通知移動(我, 列, 行):
        if 我.繁忙狀態:
            return
        我.繁忙狀態 = 真
        我.遊戲.模型.通知移動(列, 行)
        我.繁忙狀態 = 假


class 捻遊戲類(object):
    被創造狀態 = 0
    正在跑狀態 = 1
    遊戲結束狀態 = 2
    def __init__(我, 幕):
        我.狀態 = 捻遊戲類.被創造狀態
        我.幕 = 幕
        我.模型 = 捻遊戲模型類(我)
        我.視圖 = 捻遊戲視圖類(我)
        我.控制者 = 捻遊戲控制者類(我)


def 主函數():
    主螢幕 = turtle.幕類()
    主螢幕.模式("standard")
    主螢幕.設立(幕寬常數, 幕高常數)
    nim = 捻遊戲類(主螢幕)
    return "EVENTLOOP"

if __name__ == "__main__":
    主函數()
    turtle.主迴圈()

# Above: "tc_nim.py", by Renyuan Lyu (呂仁園), 2015-01-27
# Original: "nim.py", by Gregor Lingl. 


```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com
