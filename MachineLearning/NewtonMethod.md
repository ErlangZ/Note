# 牛顿法
牛顿法的原理基本上就是任意在函数上取一点，求这一点的切线和X轴的交点，再从交点位置再伸出一点继续进行
迭代。这样可以找到函数导数为0的点，就是极值,使得$\theta^{(t)} = \theta^{(t-1)}$
$$\theta^{(t)} = \theta^{(t-1)} - \frac{f(\theta^t)}{f'(\theta^{t-1})} $$


