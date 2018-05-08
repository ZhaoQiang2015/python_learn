# Pyplot
##1. Pyplot简介
- 快速绘制2D图表
##2. 简单例子
- y=x的一条直线
```python
import matplotlib.pyplot as plt
plt.plot(range(5), linestyle='--', linewidth=3, color='purple')
plt.ylabel('Numbers from 1-5')
plt.xlabel('ladfla')
plt.show()
```

##3. 常用设置方法
- `plt.title()` 图的标题
- `plt.xlabel()` x轴的名称
- `plt.ylabel()` y轴的名称

##4. 控制线条属性
- `linewidth`: 设置线宽
- 