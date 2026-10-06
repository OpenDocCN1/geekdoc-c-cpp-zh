
在修改 x 轴和 z 轴之后。
在修改 `rotationX` 变量以及 `rotationY` 或 `rotationZ` 变量后，我们调用 `updateGL()` 来重新绘制场景。

```cpp
void Tetrahedron::mouseDoubleClickEvent(MouseEvent *event) {
    int face = faceAtPosition(event->pos());
    if (face != -1) {
        QColor color = QDialog::getColor(faceColors[face], this);
        if (color.isValid()) {
            faceColors[face] = color;
            updateGL();
        }
    }
}
```

`mouseDoubleClickEvent()` 是从 QWidget 实现的，允许用户通过双击来设置四面体面的颜色。我们调用私有函数 `faceAtPosition()` 来确定光标下是否存在某个面。如果双击了某个面，我们调用 `QDialog::getColor()` 为该面获取新颜色。然后，我们用新颜色更新 `faceColors` 数组，并调用 `updateGL()` 重新绘制场景。

```cpp
int Tetrahedron::faceAtPosition(const QPoint &pos) {
    const int MaxSize = 512;
    GLuint buffer[MaxSize];
    GLuint viewport[4];

    makeCurrent();
    glGetIntegerv(GL_VIEWPORT, viewport);
    glSelectBuffer(MaxSize, buffer);
    glRenderMode(GL_SELECT);

    glInitNames();
    glPushName(0);

    glMatrixMode(GL_PROJECTION);
    glPushMatrix();
    glLoadIdentity();
    gluPickMatrix(GLdouble(pos.x()), GLdouble(viewport[3]) - pos.y()),
```

```cpp
float x = glfloat(width) / height;
glFrustum(-x, x, -1.0, 1.0, 4.0, 15.0);
draw();
glMatrixMode(GL_PROJECTION);
glPopMatrix();
```

```cpp
if (!glRenderMode(GL_RENDER)) {
    return -1;
}
return buffer[3];
```

`faceAtPosition()` 函数返回 widget 上某位置的面索引。

以下是应用程序的 `main()` 函数：

```cpp
int main(int argc, char *argv[]) {
    QApplication app(argc, argv);

    if (!QGLFormat::hasOpenGL()) {
        std::cerr << "This system has no OpenGL support" << std::endl;
    }
```

```cpp
Tetrahedron tetrahedron;
tetrahedron.setWindowTitle(QObject::tr("Tetrahedron"));
tetrahedron.resize(300, 300);
tetrahedron.show();
```

```cpp
return app.exec();
}
```

如果用户的系统不支持 OpenGL，我们将向控制台打印错误消息并立即返回。
要将应用程序与 QtOpenGL 模块以及系统的 OpenGL 库链接，`.pro` 文件需要此条目：

```pro
QT += opengl
```

四面体应用程序到此完成。

# 结合 OpenGL 和 QPainter

在上一节中，我们看到了了如何使用 OpenGL 命令在 QWidget 上绘制 3D 场景。也可以使用 QPainter 在 QWidget 上绘制 2D 图形。我们在本节中将看到的“元音立方体”（Vowel Cube）示例结合了 OpenGL 调用和 QPainter，展示了如何取两者之长。它还演示了 `QWidget::renderText()` 函数的使用，该函数允许我们在 3D 场景上绘制变换后的文本注释。应用程序如图 20.2 所示。

# 图 20.2 元音立方体应用程序

![](img/5a524abdf0b0d58fa99d30abb4463611_781_0.png)

元音立方体显示了一个带有土耳其语八个元音的立方体——这在土耳其语语法和语言书籍书中常见。图例列出了元音类别以及哪些元音属于哪个类别。立方体使得这些信息更加视觉化；例如，前元音显示在立方体的正面，后元音显示在背面。对于背景，我们使用了径向渐变。

代码视图：

```cpp
class VowelCube : public QWidget
{
    Q_OBJECT
```

public:
    VowelCube(QWidget parent = 0);
    ~VowelCube();

protected:
    void paintEvent(QPaintEvent event);
    void mousePressEvent(MouseEvent event);
    void mouseMoveEvent(MouseEvent event);
    void wheelEvent(QWheelEvent event);

private:
    void createGradient();
    void createGLObject();
    void drawBackground(QPainter painter);
    void drawCube();
    void drawLegend(QPainter *painter);

    GLuint glObject;
    QRadialGradient gradient;
    GLfloat rotationX;
    GLfloat rotationY;
    GLfloat rotationZ;
    GLfloat scaling;
    QPoint lastPos;
```

`VowelCube` 类派自 QGLWidget。它使用 `QPainter` 绘制背景渐变，然后使用 OpenGL 调用绘制立方体，接着使用 `renderText()` 在立方体的顶点绘制八个元音，最后使用 `QPainter` 和 `QTextDocument` 绘制图例。用户可以通过按下鼠标按钮、拖拽以及滚动滚轮来旋转立方体。

与上一节的四面体示例不同，在上一节中我们重新实现了高层 QGLWidget 函数 `initializeGL()`、`resizeGL()` 和 `paintGL()`，而这次我们重新实现了传统的 `QWidget` 处理器。这让我们对 OpenGL 框架有了更多的控制。以下是 `VowelCube` 构造函数：

```cpp
VowelCube::VowelCube(QWidget *parent)
    : QGLWidget(parent)
{
    setFormat(QGLFormat(SampleBuffers));
    rotationX = -3.0;
    rotationY = -5.0;
    rotationZ = 0.0;
    scaling = 1.0;

    createGradient();
    createGLObject();
}
```

在构造函数中，我们调用 `QGLWidget::setFormat()` 指定支持抗锯齿的 OpenGL 格式。然后初始化类的变量。最后，我们调用 `createGradient()` 设置径向渐变填充背景，并调用 `createGLObject()` 创建 OpenGL 对象。通过在构造函数中执行这些操作，当我们需要重新绘制场景时可以获得更好的结果。

```cpp
void VowelCube::createGradient(){
    gradient.setCoordinateMode(Gradient::Object);
    gradient.setCenter(0.45, 0.5);
    gradient.setFocalPoint(0.4, 0.45);
    gradient.setColorAt(0.0, QColor(105, 146, 182));
    gradient.setColorAt(0.4, QColor(81, 133, 150));
    gradient.setColorAt(0.8, QColor(16, 56, 121));
}
```

在 `createGradient()` 中，我们只需设置径向渐变以使用不同的色调。`setCoordinateMode()` 确保中心和焦点的坐标相对于 widget 的大小。位置是 0 到 1 之间的浮点值，其中 0 对应焦点，1 对应渐变定义的边界。

```cpp
void VowelCube::createGLObject(){
    makeCurrent();
    glShade(GL_FLAT);
    glObject = glGenLists(1);
    glLists(glObject, GL_COMPILE);
    glBegin(GL_LINES);
    glLineWidth(1.0);
    glVertex3f(1.0, 1.0, -1.0);
    glVertex3f(-1.0, 1.0, -1.0);
    glVertex3f(-1.0, -1.0, -1.0);
    glVertex3f(1.0, -1.0, -1.0);
    glEnd();
}
```

`createGLObject()` 创建了一个存储线条的列表。

```cpp
VowelCube::~VowelCube() {
    makeCurrent();
    glDeleteLists(glObject, 1);
}
```

在析构函数中，我们调用 `glDeleteLists()` 删除构造函数中创建的对象。同样，我们必须调用 `makeCurrent()`。

```cpp
void VowelCube::paintEvent(QPaintEvent event) {
    QPainter painter(this);
    drawBackground(&painter);
    drawCube();
    drawLegend(&painter);
}
```

在 `paintEvent()` 中，我们像平常 widget 那样设置 `QPainter`；然后绘制背景、立方体和图例。

```cpp
void VowelCube::drawBackground(QPainter *painter) {
    painter->setPen(Qt::NoPen);
    painter->setBrush(gradient);
    painter->drawRect(rect());
}
```

绘制背景只需使用合适的画刷调用 `rect()`。

```cpp
void VowelCube::drawCube() {
    glPushAttrib(GL_ALL_ATTRIB_BITS);
    glMatrixMode(GL_PROJECTION);
    glPushMatrix();
    glIdentity();
    float x = glfloat(width()) / height();
    glOrtho(-x, x, -3.0, 3.0, 4.0, 15.0);
    glMatrixMode(GL_MODELVIEW);
    glPushMatrix();
    glIdentity();
    glTranslatef(0.0, 0.0, -10.0);
    glScalef(scaling, scaling, scaling);
    glRotatef(rotationX, 1.0, 0.0, 0.0);
    glRotatef(rotationY, 0.0, 1.0, 0.0);
    glRotatef(rotationZ, 0.0, 0.0, 1.0);

    Enable(GL_MULTISAMPLE);
    glCallList(glObject);
    setFont(QFont("Times", 24));
    glColor(QColor(255, 223, 127));
    renderText(+1.1, +1.1, +1.1, QChar('a'));
    renderText(-1.1, +1.1, +1.1, QChar('e'));
    renderText(-1.1, +1.1, -1.1, QChar('o'));
    renderText(-1.1, +1.1, -1.1, QChar(0x00F6));
    renderText(-1.1, +1.1, +1.1, QChar(0x0131));
    Disable(GL_MULTISAMPLE);
    glPopMatrix();
    glPopMatrix();
    glPopAttrib(GL_ALL_ATTRIB_BITS);
}
```

`drawCube()` 函数是 widget 的核心。我们将分两部分进行审查：

```cpp
void VowelCube::drawLegend(QPainter *painter) {
    painter->setPen(Qt::NoPen);
    painter->setBrush(Qt::white);
    // ... (omitted for brevity)
}
```

