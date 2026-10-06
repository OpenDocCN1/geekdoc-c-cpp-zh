
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

The `faceAtPosition()` function returns the number of the face at a certain position on the widget, -1 if there is no face at that position. The code for determining this in OpenGL is a bit complicated. Essentially, we render the scene in `GL_SELECT` mode to take advantage of OpenGL's picking capabilities and then retrieve the face number ("name") of the OpenGL hit record. The code is all standard OpenGL code, except for the `QWidget::getCurrent()` call at the beginning, which is necessary to ensure that we use the correct OpenGL context. (QWidget does this automatically before it calls `initializeGL(), resizeGL(), or paintGL()`, so we don't need this call anywhere else in the Tetrahedron implementation.)

Here's the application's `main()` function:

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

If the user's system doesn't support OpenGL, we print an error message to the console and return immediately.
To link the application against the QtOpenGL module and the system's OpenGL library, the `.pro` file needs this entry:

```pro
QT += opengl
```

That completes the Tetrahedron application.

## 20. 3D Graphics

![](img/5a24abdf0b58fa99d30abb46311_773_0.png)

- Drawing Using OpenGL
- Combining OpenGL and QPainter
- Doing Overlays Using Framebuffer

OpenGL is a standard API for rendering 3D graphics. Qt applications can draw 3D graphics using the QtOpenGL module, which relies on the system's OpenGL library. The module provides the `QGLWidget` class, which we can subclass to develop our own widgets that draw themselves using OpenGL commands. For many 3D applications, this is sufficient. The first section of this chapter presents a simple application that uses this technique to draw a tetrahedron and lets the user interact with it using the mouse.

Starting with Qt 4, it is possible to use QPainter on QGLWidget as though it were a normal QWidget. One huge benefit of this is that we get the performance of OpenGL for most drawing operations, such as transformations and mapping. Another benefit of using QPainter is that we can use its higher-level API for 2D graphics, and combine it with OpenGL to perform 3D graphics in the same widget using a mixture of QPainter and OpenGL.

Using `QGLWidget`, we can draw 3D scenes on the screen, using OpenGL as the backend. To render a hardware-accelerated off-screen surface, we can use framebuffer object extensions, which are available through `QGLPixelBuffer` and `QGLFramebuffer` classes. In the third section of the chapter, we will show how to use a framebuffer object to implement layers. This chapter assumes that you are familiar with OpenGL. If OpenGL is new to you, a good place to start is http://www.opengl.org/.

## Drawing Using OpenGL

Drawing graphics with OpenGL from a Qt application is straightforward: we must subclass `QGLWidget`, reimplement a few virtual functions, and link the application against the QtOpenGL libraries. Because `QGLWidget` is derived from `QWidget`, most of what you know will apply. The main difference is that we use standard OpenGL functions to perform the drawing instead of QPainter. We will review the code of the Tetrahedron application shown in Figure 20.1, with each face drawn a different color. The user can rotate the tetrahedron by pressing a mouse button and dragging. The user can set the color of a face by double-clicking it and choosing a color from the `QDialog` that pops up.

### Figure 20.1. The Tetrahedron application

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

The Tetrahedron class is derived from `QGLWidget`. The `initializeGL()`, `resizeGL()`, and `paintGL()` functions are reimplemented from `QGLWidget`. The mouse event handlers are reimplemented from `QGLWidget` as usual.

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

In the constructor, we call `QGLWidget::setFormat()` to specify the OpenGL context, and we initialize the class's private variables.

```cpp
void Tetrahedron::initializeGL()
{
    glClearColor(Qt::black);
    glShadeModel(GL_FLAT);
    glEnable(GL_DEPTH_TEST);
    glEnable(GL_CULL_FACE);
}
```

The `initializeGL()` function is called just once, before `paintGL()` is called. This is the place where we can set up the OpenGL rendering context, define display lists, and perform other initializations.

All the code is standard OpenGL, except for the call to `QGLWidget`'s `glClearColor()` function. If we wanted to stick to standard OpenGL, we would use `glClearColor()` in RGBA mode and `glClearIndex()` in color index mode instead.

```cpp
void Tetrahedron::resize(int width, int height)
{
    glviewport(0, 0, width, height);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    GLfloat x = GLfloat(width) / height;
    glFrustum(-x, +x, -1.0, +1.0, 4.0, 15.0);
    glMatrixMode(GL_MODELVIEW);
}
```

The `resizeGL()` function is called the first time, but after `initializeGL()`. It is the place we can set up the OpenGL viewport and any other settings that depend on the widget size.

```cpp
void Tetrahedron::paintGL()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    draw();
}
```

The `paintGL()` function is called whenever the widget needs to be repainted. Code:

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

The `draw()` function performs the actual drawing of the tetrahedron. It uses the rotation angles to rotate the coordinate and then draws the four triangular faces.

```cpp
void Tetrahedron::mousePressEvent(QMouseEvent event) {
  lastPos = event->pos();
}
```

```cpp
void Tetrahedron::mouseMove(QMouseEvent event) {
  GLfloat dx = GLfloat(event->pos().x() - lastPos.x()) / width();
  GLfloat dy = GLfloat(event->pos().y() - lastPos.y()) / height();
  if (event->buttons() & Qt::LeftButton) {
    rotationX += dy * 50.0;
    rotationY += dx * 50.0;
  } else if (event->buttons() & Qt::RightButton) {
    rotationX += dy * 50.0;
    rotationZ += dx * 50.0;
  }
  update();
  lastPos = event->pos();
}
```
