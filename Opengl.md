# OpenGl

## OpenGl3D的矩阵[^1]
  投影变换即定义一个可视空间，可视空间以外的物体不会被显示到屏幕上。

### 齐次坐标(Homogeneous coordinates)
  我们用一个三元组表示一个三维的点，现在引入第4个参数w, (x, y, z, w)。(x, y, z, 1)是空间中的一个位
  置。 (x, y, z, 0)是3维空间中的一个方向。对于旋转操作来说，这个改动不会有任何的影响，但是对于一个
  平移操作，结果就会大不相同。
```cpp
 void glMatrixMode(GLenum mode);
 // GL_MODELVIEW(inital value): Applies subsequent matrix operations to the modelview matrix stack.
 // GL_PROJECTION: Applies subsequent matrix operations to the projection matrix stack.
 // GL_TEXTURE: Applies subsequent matrix operations to the texture matrix stack.
 // GL_COLOR: Applies subsequent matrix operations to the color matrix stack.
```

### Model, View and Projection matrices
  Model Coordinate 代表了一个障碍物的坐标系, 比如我们要显示一只猴子的图像，那么这只猴子的所有点都处
  在这个坐标系中。如果我们进行 `model_coord = model_coord * translation * rotation * scale;`, 那么
  猴子的影像就会被平移，旋转和缩放。
  到目前为止猴子的坐标并非在世界坐标系中，如果我们想获得世界坐标系，那么
  `world_coord =  model_matrix * model_coord;`

  View Coordinate 代表了摄像机的坐标系，我们的影像在显示到屏幕上之前会被映射到相机坐标系。
  `camera_coord = view_matrix * world_coord;`
  我们有个比较有用的函数叫`glm::lookAt` 和 `glm::translate`
```cpp
glm::mat4 CameraMatrix = glm::lookAt(
        cameraPosition, // The position of your camera, in world space
        cameraTarget,   // Where you want to look at, in world space
        upVector        // Probably glm::vec3(0,1,0), but (0,-1,0) would
                        // make you looking upside-down, which can be great too
        );
glm::mat4 ViewMatrix = glm::translate(-3.0f, 0.0f ,0.0f);
```

  经过上边的转换， 我们现在位于相机空间中，就是说如果一个点(0, 0) 是应该显示在屏幕的正中心位置上的。
  但是，我们还不能仅仅通过x, y值就决定一个物体在屏幕上的为止，z的值也很关键。如果两个点有相近的xy坐
  标，那么z值较大的那个应该离屏幕中心更近。-- 这种视角被称为透视视角, 我们有相应的函数可以做到这个
  转换。`homogeneous_coord = projection_matrix * camera_coord;`
```cpp
  // Generates a really hard-to-read matrix, but a normal, standard 4x4 matrix nonetheless
  glm::mat4 projectionMatrix = glm::perspective(
      FoV,         // The horizontal Field of View, in degrees : the amount of "zoom".
                   // Think "camera lens". Usually between 90° (extra wide) and 30° (quite zoomed in)
      4.0f / 3.0f, // Aspect Ratio. Depends on the size of your window. Notice that 4/3 ==
                   // 800/600 == 1280/960, sounds familiar ?
      0.1f,        // Near clipping plane. Keep as big as possible, or you'll get precision issues.
      100.0f       // Far clipping plane. Keep as little as possible.
      );
```

  综上，我们最终的转换矩阵是
```cpp
glm::mat4 MVPmatrix = projection * view * model; // Remember : inverted !
```

## 透视视角 (glPersepctive)[^2]

```cpp
glMatrixMode (GL_MODELVIEW);
glLoadIdentity();
gluLookAt(eyex, eyey, eyez, pX, pY, pZ, upX, upY, upZ);
```
  如上的三行代码让OpenGl使用透视视角进行显示。透视视角的景视体实际上是一个截头棱锥体(frustum)。用户
  的eye(或者叫camera)，用户视线指向p点，最后一个元素说明整个视角的正上方方向。 3D空间中的z轴是向前
  的，从eye指向p点方向，y轴方向是up方向，x轴方向是同z轴和y轴都垂直的方向。


## 平行视角 (glOrtho)
  关于平行视角的效果，可以参见

  ![平行透视](https://upload.wikimedia.org/wikipedia/commons/thumb/4/41/Graphical_projection_comparison.png/600px-Graphical_projection_comparison.png)

```cpp
glMatrixMode (GL_PROJECTION)
glLoadIdentity();
glOrtho(left, right, bottom, top, near, far);
```
  如上的三行代码让OpenGl使用平行视角进行显示。平行视角的景视体实际上是一个长方体。就是用垂直于视平面线
  进行投影看，前4个参数说明3D空间是如何被投影的, 后两个参数说明景深。可以把平行视角想象成透过一根长
  长的管道来观察3维世界，只有在管子中的near-far之间的物体才能被观察到。而管子的长度/宽度和位置就是通
  过前4个参数来指定的，在管子中的物体是没有深度信息的。不论如何调整远近距离，所有的点的图像都不变。

[^1]: http://www.opengl-tutorial.org/beginners-tutorials/tutorial-3-matrices/
[^2]: http://www.cs.umd.edu/class/sum2003/cmsc427/pSpecify.pdf

