# 深度学习的求解算法
# 随机梯度下降法

# Batch Normalization[^1]
使用mini-batches用例，相对于每次只使用一个用例有很多优点: 首先，每次迭代的梯度其实都是整体数据集梯度
的一个估计值，增大batch数量会使得这个`估计`更准确。其次，batch更大，计算也会更快。虽然SGD简单高效，
但是它对数据初始值和适当学习率的依赖很严重。

[^1]: Batch Normalization:Accelerating Deep Network Training by Reducing Internal Convaiate Shift.

