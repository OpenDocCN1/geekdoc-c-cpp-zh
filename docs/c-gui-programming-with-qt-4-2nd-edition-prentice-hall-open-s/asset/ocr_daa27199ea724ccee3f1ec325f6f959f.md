```
class Teapots : public QWidget
{
    Q_OBJECT

public:
    Teapots(QWidget parent = 0);
    ~Teapots();

protected:
    void initializeGL();
    void resizeGL(int width, int height);
    void paintGL();
    void mousePressEvent(QMouseEvent event);
    void mouseMoveEvent(QMouseEvent event);
    void mouseReleaseEvent(QMouseEvent event);

private:
    void createGLTeapotObject();
    void drawTeapot(GLfloat x, GLfloat y, GLfloat ambientR,
                    GLfloat ambientG, GLfloat ambientB,
                    GLfloat diffuseR, GLfloat diffuseG,
                    GLfloat diffuseB, GLfloat specularR,
                    GLfloat specularG, GLfloat specularB,
                    GLfloat shininess);

    void drawTeapots();
    QGLFramebufferObject *fbObject;
    QGluTeapotObject;
    QPoint rubberBandCorner1;
    QPoint rubberBandCorner2;
    bool rubberBandIsShown;

};
```

The Teapots class is derived from QWidget and reimplements the high-level OpenGL handlers initializeGL(), resizeGL(), and paintGL(). It also reimplements mousePressEvent(), mouseMove(), and mouseReleaseEvent() to let the user draw a rubber band.

The private functions take care of creating the teapot object and drawing teapots. The code is rather complex and is based on the teapots example in OpenGL Programming Guide by Jackie Noble, Tom Davis, and Mason Woo (Addison-Wesley, 1993). Since it is not directly relevant to our purposes, we will not present it here.