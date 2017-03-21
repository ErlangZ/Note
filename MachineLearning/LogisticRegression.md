# Logistics回归[^1]

## 为什么$(y-\theta x)^2/2$的损失函数使用了极大似然估计
假设我们要预测一栋房屋的价格，$\mathbf x$表示房屋的特征，$y$表示房屋的特征，我们用线性回归的方法，
$$y = \mathbf{\theta}\mathbf{x} + \epsilon$$
$\epsilon$表示训练误差，它可能来自我们没有考虑到的特征，可能来自我们的模型假设（也许它不是线性的），
还可能来自某些随机的因素，比如卖家的心情。我们假设$\epsilon$满足正态分布,那么$y|(\mathbf x;\mathbf\theta) \sim N(\mathbf\theta \mathbf x, \sigma)$
$\theta$这里是一个固定数值的量，而并不是一个随机变量。
$$P(\mathbf y|\mathbf x; \theta) = \frac{1}{\sqrt{2\pi}\sigma}exp(-\frac{(y-\mathbf \theta \mathbf x)^2}{2\sigma^2})$$
现在的问题是，怎么确定$\theta$的值，使得随机误差最小。我们使用`极大似然估计`--选择$\theta$使得
$L(\theta)$最大。就是说，固定一组$\theta$，在输入是$\mathbf x$的时候，正确的输出是$\mathbf y$的可能
性最大。我们假设各组样本误差之间是`独立同分布`的。
$$max \ L(\theta)=P(\mathbf y|\mathbf x; \theta)=\prod^m_{i=1} P(y^{(i)}|x^{(i)};\mathbf{\theta})$$
对上式取对数
$$\begin{aligned}
max \ log(L(\theta)) &= \sum^m_{i=1}log\frac{1}{\sqrt{2\pi}\sigma}exp(-\frac{(y^{(i)} -\mathbf\theta x^{(i)})^2}{2\sigma^2}) \\
                     &= m\ log\frac{1}{\sqrt{2\pi}\sigma} -\sum^m_{i=1}\frac{(y^{(i)} -\mathbf\theta x^{(i)})^2}{2\sigma^2}
\end{aligned}$$
这样，我们可以发现$max \ L(\theta)$等同于将$min \ \sum_{i=1}^m\frac{(y^{(i)}-\theta x^{(i)})^2}{2}$



## Sigmoid函数

假设
$$h(x) = \frac{1}{1+exp^{-\theta x}} $$
并且这时$y$只有两种取值, $y\in\{0,1\}$。那么
$$P(y=1|x;\theta) = h_{\theta}(x)$$
$$P(y=0|x;\theta) = 1 - h_{\theta}(x)$$
就是说，$h_{\theta}(x)$是模型预期(预测正确)是1的概率。
整理一下
$$
\begin{aligned}
P(y|x;\theta) &= (h_{\theta}(x))^y + (1 - h_{\theta}(x))^{1-y} \\
              &= \prod_{i=1}^m \ (h_{\theta}(x_{(i)}))^y_{(i)} + (1 - h_{\theta}(x_{(i)}))^{1-y_{(i)}}
\end{aligned}$$
仍然取对数
$$
max \ l(\theta) = logL(\theta) = \sum_{i=1}^m \ y^{(i)}log(h_{\theta}(x_{(i)})) + (1-y^{(i)})log(1-h_{\theta}(x_{(i)}))
$$
为了求得$l(\theta)$的最大值，我们需要知道
$$\frac{\partial{l(\theta)}}{\partial \theta} = \sum_{i=1}^m(y-h_{\theta}(x^{(i)}))x^{(i)}$$
然后，使用梯度上升算法，不断提高$L(\theta)$的值，达到比较满意的精度。

[^1]: 斯坦福N.G 网易公开课 第三节 过拟合与欠拟合
