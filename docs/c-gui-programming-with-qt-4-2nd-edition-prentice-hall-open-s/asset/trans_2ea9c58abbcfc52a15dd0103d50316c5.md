

```cpp
float x = GLfloat(width) / height();
glFrustum(-x, x, -1.0, 1.0, 4.0, 15.0);
draw();
glMatrixMode(GL_PROJECTION);
glPopMatrix();

if (!glRenderMode(GL_RENDER)) {
    return -1;
}
return buffer[3];
```

`faceAtPosition()` 函数返回小部件上特定位置的面索引，如果该位置没有面，则返回 -1。在 OpenGL 中确定此点的代码有点复杂。本质上，我们在 `GL_SELECT` 模式下渲染场景，以利用 OpenGL 的拾取（picking）能力，然后获取 OpenGL 命中记录的脸编号（“名称”）。这些代码全部是标准的 OpenGL 代码，但开头的 `QWidget::getCurrent()` 调用除外，该调用对于确保我们使用了正确的 OpenGL 上文是必要的。（QWidget 在调用 `initializeGL()`、`resizeGL()` 或 `paintGL()` 之前会自动完成这一点，因此我们不需要在 Tetrahedron 实现的其他任何地方调用此函数。）

以下是应用程序的 `main()` 函数：

```cpp
int main(int argc, char *argv[]) {
    QApplication app(argc, argv);

    if (!QGLFormat::hasOpenGL()) {
        std::cerr << "This system has no OpenGL support" << std::endl;
        return 1;
    }

    Tetrahedron tetrahedron;
    tetrahedron.setWindowTitle(QObject::tr("Tetrahedron"));
    tetrahedron.resize(300, 300);
    tetrahedron.show();

    return app.exec();
}
```

如果用户的系统不支持 OpenGL，我们将向控制台打印错误消息并立即返回。
为了将应用程序与 QtOpenGL 模块以及系统的 OpenGL 库链接，`.pro` 文件需要此条目：

```pro
QT += opengl
```

Tetrahedron 应用程序到此。

## 20. 3D 图形

![](img/5a24abdf0b58fa99d30abb46311_773_0.png)

- 使用 OpenGL 绘图
- 结合 OpenGL 和 QPainter
- 使用帧缓冲区（Framebuffer）制作叠加层

OpenGL 是用于渲染 3D 图形的标准 API。Qt 应用程序可以使用 QtOpenGL 模块绘制 3D 图形，该模块依赖于系统的 OpenGL 库。该模块提供了 `QGLWidget` 类，我们可以对其进行子类化，开发自己的使用 OpenGL 命令绘制的控件。对于许多 3D 应用程序，这足够了。本章的第一节介绍了一个简单的应用程序，它使用该技术绘制四面体，并允许用户使用鼠标与其交互。

从 Qt 4 开始，可以在 QGLWidget 上使用 QPainter，就像对待一个普通的 QWidget 一样。这样做的一个巨大好处是，我们在大多数绘制操作（如变换和映射）中获得了 OpenGL 的性能。使用 QPainter 的另一个好处是我们可以使用它的高级 API 处理 2D 图形，并与 OpenGL 结合，在同一个小部件中使用混合 QPainter 和 OpenGL 来执行 3D 图形渲染。

使用 `QGLWidget`，我们可以使用 OpenGL 作为后端在屏幕上绘制 3D 场景。要渲染硬件加速的离屏表面，可以使用帧缓冲区对象扩展，这些扩展通过 `QGLPixelBuffer` 和 `QGLFramebuffer` 类提供。在本章的第三节中，我们将展示如何使用帧缓冲区对象来实现层。本章假设你已经熟悉 OpenGL。如果 OpenGL 对你来说是新的，一个很好的起点是 http://www.opengl.org/。

## 使用 OpenGL 绘图

在 Qt 应用程序中使用 OpenGL 绘图是简单的：我们必须子类 `QGLWidget`，重新实现几个虚函数，并将应用程序与 QtOpenGL 库链接。由于 `QGLWidget` 派自于 `QWidget`，你熟悉的大部分内容都适用。主要区别在于使用标准的 OpenGL 函数执行绘制，而不是 QPainter。我们将回顾图 20.1 所示 Tetrahedron 应用程序的代码，每个面绘制有不同的颜色。用户可以通过按下鼠标按钮并拖动来旋转四面体。用户可以通过双击面并从弹出的 `QDialog` 中选择颜色来设置该面的颜色。

### 图 20.1. 四面体应用程序

![](img/5a24abdf0b58fa99d30abb46311_774_0.png)

```cpp
class Tetrahedron : public QGLWidget
{
    Q_OBJECT

public:
    Tetrahedron(QWidget parent = 0);

protected:
    void initializeGL();
    void resizeGL(int width, int height);
    void paintGL();
    void mousePressEvent(QMouseEvent event);
    void mouseMoveEvent(QMouseEvent event);
    void mouseDoubleClickEvent(QMouseEvent event);

private:
    void draw();
    int faceAtPosition(const QPoint &pos);

    GLfloat rotationX;
    GLfloat rotationY;
    GLfloat rotationZ;
    QColor faceColors[4];
    QPoint lastPos;
};
```

Tetrahedron 类派自 `QGLWidget`。`initializeGL()`、`resizeGL()` 和 `paintGL()` 函数是从 `QGLWidget` 重新实现的。鼠标事件处理也像往常一样从 `QGLWidget` 重新实现。

```cpp
Tetrahedron::Tetrahedron(QWidget *parent)
    : QGLWidget(parent)
{
    setFormat(QGLFormat(QGL::DoubleBuffer | QGL::DepthBuffer));
    rotationX = -21.0;
    rotationY = -57.0;
    rotationZ = 0.0;
    faceColors[0] = Qt::red;
    faceColors[1] = Qt::green;
    faceColors[2] = Qt::blue;
    faceColors[3] = Qt::yellow;
}
```

在构造函数中，我们调用 `QGLWidget::setFormat()` 来指定 OpenGL 上文，并初始化类的私有变量。

```cpp
void Tetrahedron::initializeGL()
{
    glClearColor(Qt::black);
    glShadeModel(GL_FLAT);
    glEnable(GL_DEPTH_TEST);
    glEnable(GL_CULL_FACE);
}
```

`initializeGL()` 函数在 `paintGL()` 调用之前调用一次。这是我们可以设置 OpenGL 渲染上文、定义显示列表并进行其他初始化的地方。

所有代码都是标准的 OpenGL，对 `QGLWidget` 的 `glClearColor()` 调用除外。如果我们坚持使用标准 OpenGL，会在 RGBA 模式下使用 `glClearIndex()` 而不是颜色模式。

```cpp
void Tetrahedron::resize(int width, int height)
{
    glviewport(0, 0, width, height);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    GLfloat x = GLfloat(width) / height;
    glFrustum(-x, x, -1.0, 1.0, 4.0, 15.0);
    glMatrixMode(GL_MODELVIEW);
}
```

`resizeGL()` 函数第一次调用，在 `initializeGL()` 之后。这是我们可以设置 OpenGL 口以及任何依赖于小部件尺寸设置的地方。

```cpp
void Tetrahedron::paintGL()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    draw();
}
```

`paintGL()` 函数在小部件需要重绘时被调用。代码：

```cpp
void Tetrahedron::draw()
{
    glMatrixMode(GL_MODELVIEW);
    glLoadIdentity();
    glTranslatef(0.0, 0.0, -10.0);
    glRotatef(rotationX, 1.0, 0.0, 0.0);
    glRotatef(rotationY, 0.0, 1.0, 0.0);
    glRotatef(rotationZ, 0.0, 0.0, 1.0);

    for (int i = 0; i < 4; i++) {
      glBegin(GL_TRIANGLES);
        glColor(faceColors[i]);
        for (int j = 0; j < 3; j++) {
          glVertex3f(coords[i][j][0], coords[i][j][1], coords[i][j][2]);
        }
      glEnd();
    }
}
```

`draw()` 函数执行四面体的实际绘制。它使用旋转角度旋转坐标，然后绘制四个三角形面。

