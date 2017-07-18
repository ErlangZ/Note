# Point set registration

## Iterative Closest Point (ICP)[^1]
ICP算法用来最小化两帧点云之间的差异. ICP算法会迭代的对姿态矩阵进行转换，逐步的降低两帧之间的误差．
这里的误差通常是用从基准点到原点之间的差异来决定的．ICP是应用最广泛的进行三维空间对齐的方法．

算法的内容
```
Input: 参考点$R$和源点云$P$,(Optional)初始的姿态估计，迭代的终止条件
Output: 重新调整过的转换关系
Step: 1. 对每个点都同它最临近的点进行匹配.
　　　2. 使用均方根方法来估计出最佳的$M$(Rotation & Translation)．
　　　3. 使用得来的转换矩阵$M$转换$P$.
      4. 迭代，重复上述过程.
```

[^1]: https://en.wikipedia.org/wiki/Iterative_closest_point
