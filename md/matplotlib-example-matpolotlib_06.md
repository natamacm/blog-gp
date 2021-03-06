---
title: matplotlib example matpolotlib 06 (snippet)
date: 2020-03-03
tags: ["python"]
---
Python matplotlib example 'matpolotlib 06'


Modules used in program: 
* `import matplotlib.pyplot as plt`
* `import numpy as np`

## python matpolotlib 06

Python matplotlib example: matpolotlib 06

```python
'''
    添加注解和绘制点以及在图形上绘制线或点
'''
import numpy as np
import matplotlib.pyplot as plt

# 绘制简单的图形
x = np.linspace(-3, 3, 50)
y = 2 * x + 1

plt.figure()

plt.plot(x, y)

#将上,右边框去掉
ax = plt.gca()
ax.spines['right'].set_color('none')
ax.spines['top'].set_color('none')

# 设置x轴的位置以及数据在坐标上对应的位置
ax.xaxis.set_ticks_position('bottom')
ax.spines['bottom'].set_position(('data', 0))

# 设置y轴的位置以及数据在坐标上对应的位置
ax.yaxis.set_ticks_position('left')
ax.spines['left'].set_position(('data', 0))



# 定义(x0, y0)点
x0 = 1
y0 = 2 * x0 + 1

# 绘制(x0, y0)点
plt.scatter(x0, y0, s=50, color='blue')
# 绘制虚线
plt.plot([x0, y0], [y0, 0], 'k--', lw=2.5)
#绘制注解一
plt.annotate(r'$2 * x + 1 = %s$' % y0, xy=(x0, y0), xycoords='data', xytext=(+30, -30), \
             textcoords='offset points', fontsize=16, arrowprops=dict(arrowstyle='->', connectionstyle='arc3, rad = .2'))
# 绘制注解二
plt.text(-3, 3, r'$Test\ text. \mu \sigma_i, \alpha_i$', fontdict={'size': 16, 'color': 'red'})

plt.show()

```

## Python links

- Learn Python: https://pythonbasics.org/
- Python Tutorial: https://pythonprogramminglanguage.com
