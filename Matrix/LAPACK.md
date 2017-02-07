# LAPack
LAPack(Linear Algebra PACKage)使用Fortarn写于上世纪90年代[^1],提供了线性代数运算的基本方法。比如，
求解线性方程, 求解最小二乘法，特征值，奇异值等问题。LAPACK使用了高效的矩阵分块算法，可以有效的进行
并行计算。  
LAPACK中的大多数算法都包含:REAL,DOUBLE,COMPLEX,COMPLEX*16四种版本，最后一种数据结果不一定所有编译器
都支持。[^2]LAPACK的方法可以分为三类：Driver方法一般用来解决比较复杂的问题，比如求解线性方程,计算实
数对称矩阵特征值等等;Computational方法也叫简单方法，一般用来处理一种计算任务，比如矩阵相乘,计算实数
三角矩阵特征值等等, Driver方法通过调用Computational方法来工作; Auxilliary方法就是被上述两种方法调用
的方法。  

# BLAS
BLAS(Basic Linear Algebra Subprograms)定义了矩阵运算的基础操作。LAPack就是围绕这操作进行设计的, 
其实LAPack的底层就是BLAS。[^3] BLAS中包含了三个级别的运算, 接口定义参见[BLAS](http://www.netlib.org/blas/#_documentation)。

 - Level1:向量乘以向量$y \gets \alpha x + y$
 - Level2:矩阵乘以向量$y \gets \alpha Ax + \beta y$和求解$x$的线性方程$Tx=y$, 这里T必须是三角矩阵。 
 - Level3:矩阵乘以矩阵, $$ C \gets \alpha AB + \beta C$$Level3也被称作GeMM(General Matrix Multiplication),
A，B矩阵可以选择是否进行转置或Hermitian共轭操作。因为很多更快的算法都可以转化为GeMM，所以GeMM成为
系统优化的主要目标。Level3中还定义了求解方程$$B\gets \alpha T^{-1} B$$的方法，这里T也表示一个三角矩阵。  


[^1]:http://www.netlib.org/lapack/
[^2]:Quick_Installation_Guide_for_LAPACK_on_Unix_Systems
[^3]:http://www.netlib.org/blas/faq.html










