# 20. 3D Graphics

![](bbox=[0.017, 0.046, 0.193, 0.143])

+   * Drawing Using OpenGL

+   * Combining OpenGL and QPainter

+   * Doing Overlays Using Framebuffer Objects

OpenGL is a standard API for rendering 3D graphics. Qt applications can draw 3D graphics by using the OpenGL module, which relies on the system's OpenGL library. The module provides the OpenGL class, which we can subclass to develop our widgets that draw themselves using OpenGL commands. For many 3D applications, this is sufficient. The first section of this chapter presents a simple application that uses this technique to draw a tetrahedron and lets the user interact with it using the mouse.

Starting with QT 4, it is possible to use QPainter on a QWidget as though it were a normal QWidget. One huge benefit of this is that we get the performance of OpenGL for most drawing operations, such as transformations and pixmap drawing. Another benefit of using QPainter is that we can use its higher-level API for 2D graphics, and combine it with OpenGL to perform 3D graphics. In the chapter's second section, we will show how to combine 2D and 3D drawing in the same widget using a mixture of QPainter and OpenGL commands.

Using QWidget, we can draw 3D scenes on the screen, using OpenGL as the back-end. To render a hardware-accelerated off-screen surface, we can use the buffer and framebuffer object extensions, which are available through the OpenGLPixelBuffer and QGLFramebufferObject classes. In the third section of the chapter, we will show how to use a framebuffer object to implement overlays.

This chapter assumes that you are familiar with OpenGL. If OpenGL is new to you, a good place to start learning it is http://www.opengl.org.

# Drawing Using OpenGL

Drawing graphics with OpenGL from a Qt application is straightforward: We must subclass QWidget, reimplement a few virtual functions, and link the application against the QtOpenGL and OpenGL libraries. Because QWidget is derived from QWidget, most of what we already know still. The main difference is that we use standard OpenGL functions to perform the drawing instead of QPainter.