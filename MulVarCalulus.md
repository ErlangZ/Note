# 多变量微积分
## 符号定义
1. 标量使用小写字母$x$; 向量使用加粗的字母$\boldsymbol{x}$。$|\boldsymbol{x}|$表示向量的长度，
   Dir($\boldsymbol{x}$)表示向量的方向。  
   矩阵使用大写字母$A$
2. 一元函数$$y=f(x)$$多元函数$$y=f(x_1,x_2,x_3,...x_n)=f(\boldsymbol{x})$$
3. 一元导数$$f'(x) = \lim_{\Delta x \to 0} \frac{f(x + \Delta x) - f(x)}{\Delta x}$$
4. 多元函数没有通常意义上的导数$d$,只有偏导数$f_x = \partial{f}/\partial{\mathbf{x}}$
   $$f_x(x_0, y_0) = \lim_{\Delta x \to 0} \frac{f(x_0+\Delta x, y_0)-f(x_0, y_0)}{\Delta x}$$
   n元函数$f(\boldsymbol{x})$的导数(n维偏导数)是一个向量
   $\frac{\partial{f}}{\partial{\boldsymbol{x}}} = [ \frac{\partial{f}}{\partial{x_1}}, \frac{\partial{f}}{\partial{x_2}},...,\frac{\partial{f}}{\partial{x_n}} ]$
   表示$(x_0, y_0)$的梯度方向。
5. 泰勒公式 $$ f(x) = \sum_{n=0}^N \frac{f^{(n)}(a)}{n!}f(x-a)^n + R_n(x) $$


## 描述3维空间中的直线,曲线和平面
$ax+by+cy=d$描述一个三维空间中的**平面**。$[a,b,c]$是过原点平面的法向量$\mathbf N$, $d$在$\mathbf N$
是单位向量时，表示原点到平面的距离；当$d=0$时,平面过原点; 当$d \ne 0$时,平面不过原点,但是平面经过P0$(x_0,y_0,z_0)$点, 
$(P-P0) \perp \mathbf N$,得到平面的参数方程$$a(x-x_0)+b(y-y_0)+c(z-z_0)=0$$
也就是说，确定3维空间中的一个平面需要6个参数：一个经过平面的点$P0$和这个平面的三维法向量$\mathbf N$。
这就是直线的另一种定义：**直线是一个移动的点**，进一步可以定义一个三维的方程组给出直线的**参数方程**:
$x=x(t)$, $y=y(t)$, $z=z(t)$。事实上，使用参数方程，我们还可以很容易的描述出各种**曲线**。 
比如$[\theta-sin\theta, 1-cos\theta]$定义了一条`摆线`。

两个3D空间中的不平行的平面，确定一条3D空间中的**直线**;三个3D空间中的平面，有可能(当法向量组成的矩
阵可逆)确定一个**点**。

空间中任意一点P'(x',y',z')到平面$ax+by+cy=d$的距离是$$\frac{|ax'+by'+cz'-d|}{\sqrt{a^2+b^2+c^2}}$$
证明:  
平面的参数为平面上一点P0$(x_0, y_0, z_0)$, $(P-P') \perp (P-P0)$,求P'到平面的距离是
$$ |P'-P_0|cos\theta = \frac{|(P'-P_0) \cdot \mathbf{N}| }{ |\mathbf{N}| }$$,
其中$\theta$是$P'-P_0$和平面法向量的夹角。



## 链式求导法则
令$z=f(x,y)$,如果$x \leadsto x + \Delta x$, $y \leadsto y + \Delta y$
$$\Delta z \leadsto f_x \Delta x + f_y \Delta y$$
证明:给定$(x_0, y_0)$点  
在$x=x_0$平面上的切线L1是$\begin{cases}x=x_0\\z=z_0+f_x(x-x_0)\end{cases}$  
在$y=y_0$平面上的切线L2是$\begin{cases}y=y_0\\z=z_0+f_y(y-y_0)\end{cases}$  
L1,L2相交构成的平面是$z=z_0+f_x(x-x_0)+f_y(y-y_0)$,这样上式就得到证明。


## 关于矩阵求导
关于多变量函数的导数，大学里很少有课程会涉及，外边的参考资料也比较少，但是这部分内容在机器学习等领域
应用的特别广泛。如下的内容就是关于对矩阵和多变量函数进行求导的。

在矩阵的范畴内，一共存在着六种不同的导数，[^2]  
标量对标量求导$\frac{dy}{dx}$,   
标量对矩阵求导$\frac{dy}{d\mathbf X}=\frac{\partial y}{\partial x_{ji}}$  
向量对标量求导$\frac{d \mathbf y}{dx}=\frac{\partial y_i}{dx}$,  
矩阵对标量求导$\frac{d \mathbf Y}{dx}=\frac{\partial y_{ij}}{\partial x}$  
向量对标量求导$\frac{dy}{d\mathbf x} =\frac{\partial y}{\partial \mathbf x_j}$  
向量对向量求导$\frac{d\mathbf y}{d \mathbf x}=\frac{\partial y_i}{\partial x_j}$   
通过上式可以看出来，向量或者矩阵并不能对比自己简单的运算进行求导，比如向量就不能对矩阵进行求导。另外,
处在分子位置上的，其实一定是一个函数，即使它是一个矩阵，也是一种多个函数组成的矩阵。

如果是对分子部分求偏导数，偏导数的Shape要依赖于$\mathbf Y$的Shape;如果并行求偏导数的部分在分母上，
偏导数的Shape则是$\mathbf X$的转置。例如,$x$$y$都是列向量，$d\mathbf y/dx$是一个列向量，而
$dy/d\mathbf x$则是一个行向量。

### 关于矩阵的微分
矩阵的微分过程实际上就同标量的微分有区别，它并不要求$x$和$y$是一个标量。定义$dy(x)$是$y(x)$在$dx$
上的微分$$\mathbf y(\mathbf x+d \mathbf x)=\mathbf y(\mathbf x) + \mathbf Ad\mathbf x + (Higher Order Terms)$$
并且$y(x+dx)$在任何位置都满足相关的连续属性。
矩阵$\mathbf A$就是导数，因为你可以保留$d\mathbf x$的任何一个分量是极小值，而把其余的分量置成零；这个
矩阵$\mathbf A$也被称作雅各布矩阵$\mathbf J_{x \to y}$。它的转置是y的梯度，使用$\nabla y$表示。这个
矩阵在计算最优化问题的解时尤其有用。所以在计算一个表达式导数的时候，可以分成两步, 1.先计算表达式的微分；
2.再将表达式转换成规范形式。

表达式的微分可以使用如下的规则进行计算：
$$\begin{aligned}
d \mathbf A &= 0 \\
d(\alpha \mathbf X) &= \alpha d \mathbf X \\
d(\mathbf X + \mathbf Y) &= d\mathbf X + d\mathbf Y \\
d(tr(\mathbf X)) &= tr(d \mathbf X)) \\
d(\mathbf X \mathbf Y) &= d(\mathbf X) \mathbf Y + \mathbf X d\mathbf Y  \\
d\mathbf X^{-1} &= -\mathbf X^{-1}d(\mathbf X)\mathbf X^{-1}
\end{aligned}$$
等等公式(参考文献中更全)[^3]，这些公式基本上都可以用$\mathbf F(\mathbf X+d\mathbf X)-\mathbf F(\mathbf X)$
然后再拿掉高阶的部分进行求解。比如
$$(\mathbf X + d \mathbf X)(\mathbf Y + d \mathbf Y) = \mathbf X \mathbf Y + (d\mathbf X)\mathbf Y + \mathbf Xd\mathbf Y + (d\mathbf X)(d \mathbf Y)$$
再比如求$d\mathbf X^{-1}$,
$$\mathbf 0 = d\mathbf I = d\mathbf X^{-1}\mathbf X=(d\mathbf X^{-1})\mathbf X + \mathbf X^{-1}d\mathbf X$$
这些公式也都可以递归的使用链式求导法则来进行计算
$$d(\mathbf A \mathbf X + \mathbf Y) = d(\mathbf A \mathbf X) + d\mathbf Y = \mathbf A d \mathbf X + d \mathbf A \mathbf X + d\mathbf Y = \mathbf A d \mathbf X + d\mathbf Y$$

计算导数的下一步是按照计算导数的六种形式将其转换成标准形式，假设$\mathbf x$和$ \mathbf y $都是列向量：

| $ dy =\alpha dx $ | $ d\mathbf y = \mathbf{\alpha} dx $ | $ d\mathbf Y = \mathbf A dx $ |
|xx|xxl|xx|

[^1]: MIT多变量微积分公开课
[^2]: Old_and_New_Matrix_Algebra_Useful_for_Statisics_from_Minka_2000
[^3]: http://www.math.uwaterloo.ca/~hwolkowi/matrixcookbook.pdf


