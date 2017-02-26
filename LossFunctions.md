# 深度学习中的损失函数
## Logistic(Sigmoid函数) + 交叉熵损失函数
在二分类问题中，训练样本为$[(\mathbf{x}^{1}, y^{1}), (\mathbf{x}^{2}, y^{2}),..., (\mathbf{x}^{n}, y^{n})]$, 
$y^{n} \in \{0, 1\}$。

假设输出函数$h_\mathbf{\theta}(\mathbf{x})$将$\mathbf{x}$映射到$[0, 1]$区间, $\mathbf{\theta}$是模型参数。
$$h_\mathbf{\theta}(\mathbf{x}) = \frac{1}{1 + e^{-\mathbf{\theta}^T\mathbf{x}}}$$
$h(\mathbf{x})$实际上是$y=1$的概率$P(y=1|\mathbf{x};\mathbf{\theta})$，$1-h(\mathbf{x})$就是$y=0$
的概率。

损失函数设计为$J(\mathbf{\theta})$, 为了将这个函数进行最小化。
$$J(\mathbf{\theta}) = \begin{cases} 
                                    -log[h_\mathbf{\theta}(\mathbf{x})] & y = 1 \\
                                    -log[1-h_\mathbf{\theta}(\mathbf{x})] & y = 0 
                      \end{cases}$$
进一步整理之后,得到交叉熵的计算公式
$$
\begin{aligned}
J(\mathbf{\theta}) &= Mean(y\{-log[h_\mathbf{\theta}(\mathbf{x})]\} + (1-y)\{-log[1-h_\mathbf{\theta}(\mathbf{x})]\}) \\
&=-Mean(ylog[h_\mathbf{\theta}(\mathbf{x})] + (1-y)log[1-h_\mathbf{\theta}(\mathbf{x})]) \\
&=-Mean(ylog[\frac{1}{1 + e^{-\mathbf{\theta}^T\mathbf{x}}}] + (1-y)log[\frac{e^{-\mathbf{\theta}^T\mathbf{x}}}{1 + e^{-\mathbf{\theta}^T\mathbf{x}}}]) \\
&=-Mean(y\mathbf\theta^T\mathbf{x} + log[\frac{e^{-\theta^T\mathbf x}}{1+e^{-\theta^T\mathbf x}}] ) \\
&=-Mean((y-1)\mathbf\theta^T\mathbf{x} - log[1+e^{-\theta^T\mathbf x}])
\end{aligned}
$$
这里有个问题，当$e^{-\mathbf x}$很大时，整个公式值很小，结果可能会溢出，为了解决这个问题Caffe在公式
的分子分母熵同时乘以了$e^{\mathbf x}$ 
$$ \begin{cases}
   \frac{e^{-\mathbf {\theta^T x}}}{1 + e^{-\mathbf{\theta}^T\mathbf{x}}} & \mathbf x > 0 \\
   \frac{1}{e^{\mathbf{\theta}^T\mathbf{x}} + 1} & \mathbf x <= 0 
   \end{cases}
$$
整个$J(\mathbf{\theta})$可以划为
$$
\begin{aligned}
J(\mathbf{\theta}) &= \begin{cases}
                      -Mean((y-1)\mathbf\theta^T\mathbf{x} - log[1+e^{-\theta^T\mathbf x}]) & \mathbf x > 0 \\
                      -Mean(y\mathbf\theta^T\mathbf{x} - log[1+e^{\theta^T\mathbf x}] & \mathbf x <= 0
                      \end{cases} \\
                   &= -Mean\{[y - (\mathbf x > 0)]\theta^T\mathbf{x} - log[1 + e^{\theta^T\mathbf x - 2 \theta^T\mathbf x (x>0)}]  \} 
\end{aligned}
$$

$J$对$\mathbf{\theta}$求导数，这是一个标量对向量求导的过程
$$\frac{\partial{J}}{\partial\mathbf\theta}
=\frac{\partial{J}}{\partial h}\frac{\partial h}{\partial\mathbf\theta}
=[\frac{y}{h}-\frac{1-y}{1-h}]h(1-h)
=y-h
$$
在实际的计算中，可能还包含了一个系数l，这就是为什么Caffe在最后进行了一次Scale。




