#卡尔曼滤波器在机器人中的应用
1950年，卡尔曼在论文中发表了一种使用递归方法，来解决线性系统的滤波和预测问题。这种方法可以在不清楚模型确切性质的情况下，使估计的均方误差最小。在机器人相关研究中，机器人的相关状态（比如机器人的准确位置、障碍物的位置等）一般都不能直接通过传感器进行测量，人们经常需要根据传感器的测量值，来推断机器人的实际状态。卡尔曼滤波就是一种常见的推断方法。
名词解释：
* belief : 表示机器人对环境状态的认识，是某种条件概率分布$p(x_t)=p(x_t|z_{1:t},u_{1:t})$。$x_t$代表状态向量，$z_t$是传感器的测量值，代表机器人对外界的感知；$u_t$是控制变量，代表外界环境对机器人的影响。

##高斯系统
  卡尔曼滤波器是一种高斯系统，高斯系统仅仅使用均值$\mu$和协方差$\Sigma$来描述系统的belief。$\mu_t$和$\Sigma_t$确定后，我们就很容易知道$x_t$状态的概率。
  高斯系统的概率密度函数：$$ p(x) = det(2\pi\Sigma)^{-\frac{1}{2}}exp^{-\frac{1}{2}(x-\mu)^T\Sigma^{-1}(x-\mu)}$$比如机器人的速度状态、位置状态都属于线性变化。这些状态$x_t$和$x_{t-1}$之间存在转换关系：$$x_t = A_tx_{t-1} + B_tu_{t} + \epsilon_t$$$x_t$是状态向量，$u_t$是控制向量。$\epsilon_t$是高斯噪声，它的均值$\mu=0$，协方差$\Sigma=R_t$。系统的belief为
$$ p(x_t|x_{t-1},u_t) = det(2\pi R_t)^{-\frac{1}{2}} *exp^{-\frac{1}{2}(x_t-A_tx_{t-1}-B_tu_t)^T*R_t^{-1}*(x_t-A_tx_{t-1}+B_tu_t)}$$ 测量值$Z_t$和真实值$X_t$之间也存在一个线性变换关系，$$z_t = C_t*x_t + \theta_t$$$\theta_t$是满足高斯分布的测量误差，均值为0，协方差为$Q_t$。
$$ p(z_t | x_t) = det(2\pi Q_t)^{-\frac{1}{2}}*exp^{-\frac{1}{2}(z_t - C_t*X_t)^TQ_t^{-1}(z_t - C_t*X_t)} $$ $$p(z_t) = p(z_t|x_t)*p(x_t)$$

### 算法步骤
$input: \mu_{t-1}, \Sigma_{t-1}, u_t, z_t$
\begin{align}
\hat{\mu_t} &= A_t\mu_{t-1} + B_tu_t\\
\hat{\Sigma_t} &= A_t\Sigma_{t-1}A_t^T + R_t\\
K_t &= \hat{\Sigma_t}C_t^T(C_t\hat{\Sigma_t}C_t^T + Q_t)^{-1} \\
\mu_t &= \hat{\mu_t} + K_t(z_t - C_t\hat{\mu_t}) \\
\Sigma_t &= (I - K_tC_t)\hat{\Sigma_t} 
\end{align}

### 算法推导
参见《Probabsibility Robotics 2005》 第3章

### 实例
  举例来说，当我们要预测在XY平面上，一个机器人的位置$P^x,P^y$和速度$V^x$$V^y$时，我们就可以用卡尔曼滤波器。
  \begin{align}P^x_t & = P^x_{t-1} + \Delta tV^x \\
  P^y_t & = P^y_{t-1} + \Delta tV^y \\
  V^x_t & = V^x_t \\
  V^y_t & = V^y_t \end{align} 
  可以写成矩阵形式$X_t = [P^x,P^y,V^x,V^y]$, $A_t = \begin{pmatrix}1 & 0 & \Delta t & 0 \\ 0 & 1 & 0 & \Delta t \\
  0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1
\end{pmatrix}$, 假设障碍物没有额外的动力系统（不会突然加速），这里$u_t$是零矩阵。可以使用卡尔曼滤波对物体状态进行预测。

