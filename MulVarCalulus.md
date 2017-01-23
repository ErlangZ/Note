# 多变量微积分
## 符号定义
1. 标量使用小写字母$x$; 向量使用加粗的字母$\boldsymbol{x}$。$|\boldsymbol{x}|$表示向量的长度，
   Dir($\boldsymbol{x}$)表示向量的方向。  
   矩阵使用大写字母$A$
2. 一元函数$$y=f(x)$$多元函数$$y=f(x_1,x_2,x_3,...x_n)=f(\boldsymbol{x})$$
3. 一元导数$$f'(x) = \lim_{\Delta x \to 0} \frac{f(x + \Delta x) - f(x)}{\Delta x}$$
4. 多元函数没有通常意义上的导数$d$,只有偏导数$f_x = \partial{f}/\partial{\boldmath{x}}$
   $$f_x(x_0, y_0) = \lim_{\Delta x \to 0} \frac{f(x_0+\Delta x, y_0)-f(x_0, y_0)}{\Delta x}$$
   对于n元函数$f(\boldsymbol{x})$，它的导数(n维偏导数)是一个n维向量
   $\frac{\partial{f}}{\partial{\boldsymbol{x}}} = [ \frac{\partial{f}}{\partial{x_1}}, \frac{\partial{f}}{\partial{x_2}},...,\frac{\partial{f}}{\partial{x_n}} ]$
   表示在某个点上的梯度方向。

## 描述3维空间中的直线和平面
$ax+by+cy=d$描述一个三维空间中的**平面**。当$d=0$时,平面过原点, $[a,b,c]$向量是过原点平面的法向量
$\mathbf N$; 当$d \ne 0$时,平面不过原点,但是平面经过P0$(x_0,y_0,z_0)$点, $(P-P0) \perp \mathbf N$,
得到平面的参数方程$$a(x-x_0)+b(y-y_0)+c(z-z_0)=0$$
两个3D空间中的不平行的平面，确定一条3D空间中的**直线**;三个3D空间中的平面，有可能(当法向量组成的矩
阵可逆)确定一个**点**。

## 链式求导法则
令$z=f(x,y)$,如果$x \leadsto x + \Delta x$, $y \leadsto y + \Delta y$
$$\Delta z \leadsto f_x \Delta x + f_y \Delta y$$
证明:给定$(x_0, y_0)$点  
在$x=x_0$平面上的切线L1是$\begin{cases}x=x_0\\z=z_0+f_x(x-x_0)\end{cases}$  
在$y=y_0$平面上的切线L2是$\begin{cases}y=y_0\\z=z_0+f_y(y-y_0)\end{cases}$  
L1,L2相交构成的平面是$z=z_0+f_x(x-x_0)+f_y(y-y_0)$,这样上式就得到证明。


