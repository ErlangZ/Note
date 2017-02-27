# 切割图像和点云数据中的障碍物
我采用了对Pixel空间进行分类的方法来解决这个问题，具体思路就是通过"反卷积[^1]"操作将被激活的特征值反
向映射回图像空间。
## 卷积神经网络的可视化
通常有两种方法来可视化神经网络[^2]，一种是直接可视化每层网络的activity,按照论文上的方法，从最后一层
激活层开始，依次经过若干次unpooling，relu和decov，将输出映射会图像空间。如果要观察某一层的特征，就
是将这一层特征的最大(或者top-k)个activity保留下来，剩下activity都赋值为0，观察图像的变化。这种方法
可以很容易的观察到灰度图的特征映射情况，但是彩色图片映射回去效果似乎不好。还有个问题是，可能有很多
的激活值都是０，这表明这个过滤器失效了，这通常也是学习率设置过高的表现。另外，我在使用AlexNet[^3]使
用Caffe实验过程中，注意Caffe自带的Deconv层需要对Net代码进行一下修改，之前训练时候的Conv权重才能被加
载到反卷积层中，否则DeConv的权重实际上一直是零值。这个Bug不容易发现。还有一种方式是可视化过滤器的权
重，通常一个训练好的模型，权重可视化后都会呈现出比较明显的模式。


[^1]:Visualizing_and_Understanding_Convolutional_Networks_from_Matthew_D._Zeiler_and_Rob_Fergu
[^2]:http://cs231n.github.io/understanding-cnn/
[^3]:https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf
[^4]:http://igva2012.wikispaces.asu.edu/file/view/Erhan+2009+Visualizing+higher+layer+features+of+a+deep+network.pdf


