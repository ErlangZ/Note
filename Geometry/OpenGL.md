# OpenGL介绍
OpenGL是一套图像硬件的接口[^1]，大约由150余条不同的命令构成。OpenGL被设计成流式的，独立于不同硬件平
台之上。为了做到这一点，其中没有任何一条命令是来执行窗口任务，或者获得用户输入的，它也不提供高层的
3D图像接口，这些都需要你自己通过OpenGl的`几何原语(比如点/线/凸包等)`进行构造。

高级一些的库可以通过OpenGl进行构造，比如GLU(OpenGl Utilty Libary)，这些库都提供了很多高级的图形，比
如二次曲面等等。GLU实际上是标准OpenGl实现的一部分，所以在OpenGl库中，同时存在上层和下层的接口。

[^1:] ftp://ftp.sgi.com/opengl/contrib/kschwarz/OPEN_GL/REFERENCE/OGL_PG/oglPG.pdf
