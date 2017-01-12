# 卷积神经网络Convolutional Networks

卷积神经网络是一类具有Grid类型拓扑的特殊神经网络[^1]，声音信号可以看做是1维Grid，图像信号可以看做是2维
Grid。比如雷达传感器收到的信号中一般都会包含噪声，我们希望能够找到一种卷积操作来过滤掉这种噪声,
$$\int x(a)w(t-a)da$$那么卷积核$w(a)$应该是多少呢？我们可以通过随机梯度下降法通过模型训练，找出一个
比较合适的卷积核。--这其实就是CNN的工作原理。

离散卷积可以看成矩阵乘法[^2]
$$\left[\begin{matrix}1&2&3&4\\5&6&7&8\\9&10&11&12\end{matrix}\right]*\left[\begin{matrix}1&0\\0&1\end{matrix}\right]$$
这个卷积运算等价于
$$\left[\begin{matrix}1&2&5&6\\2&3&6&7\\3&4&7&8\\5&6&9&10\\6&7&10&11\\7&8&11&12\end{matrix}\right] \times \left[\begin{matrix}1\\0\\0\\1\end{matrix}\right]$$
计算出来的结果，再按照每3个一行进行切割，得到2*3的特征矩阵。所以，实际上卷积神经网络的迭代算法，和全
连接网络的迭代算法，并没有本质的区别。

## 反向传播算法
系统的学习样本为共N组表示为$(X_i,Y_i), \qquad 0 \leqslant i\leqslant N$, 规定L为网络层数，
$0 \leqslant l \leqslant L, W^l$代表$l$层的权重, $b^l$是偏置, $x^l$是第l层的输入，$y$是整个网络的
输出, $$u^l=W^lx^{l-1}+b^l, \qquad x^l=f(u^l)\tag 1$$ $$y=f(W^lx^{L-1}+b^l)$$定义损失函数
$$E=\frac{1}{2}(Y-y)^2=\frac{1}{2} \sum_{i=1}^N (Y_i-y_i)^2$$ 训练时，(X,Y)都是这个方程的已知参数，
我们要找一组$W$和$b$，使得$E$最小。

使用随机梯度下降法, $\eta$是学习率
$$W^l \gets W^l - \eta \frac{\partial E}{\partial W^l}$$ 
$$b^l \gets b^l - \eta \frac{\partial E}{\partial b^l}$$
观察一下$\tag 1$,我们很容易得到下边的$\delta$,实际上，每层的误差都可以表示成$\delta$的变形。
$$\delta = \frac{\partial E}{\partial b}=\frac{\partial E}{\partial u}\frac{\partial u}{\partial b}$$
## 卷积神经网络的基本运算
- Relu
- Pooling 
   Pooling运算是一种Down-Sampling。简单的说，就是把$M \times N$的图像区域按照$K \times K$的大小进行
   划分，然后每个区域进行AVE或者MAX运算，得到$M/K \times N/K$大小的特征图像。比如原图像大小为16*16,
   我们希望进行2:1的采样，那么采用2*2的Pooling-Region大小，会得到8*8的结果图像。Pooling操作一般紧
   跟卷积层之后，它带来了某种"不变性"，就是图像中只要在某片区域中出现了某个信息就判定结果为真，而不
   要求图像每个像素点都同预期完全一致，现在主要使用的Pooling类型为Max-Pooling。
    
   问题是在反向传播的时候，Pooling的行为是怎么样的?[^3]
- Normalization
- Dropout

[^1]: https://www.deeplearningbook.org/contents/convnets.html
[^2]: https://erlangz.wordpress.com/Convolution.html






