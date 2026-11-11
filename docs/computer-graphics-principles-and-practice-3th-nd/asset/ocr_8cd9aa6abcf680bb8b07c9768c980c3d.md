```
```c
// Specify the material before specifying primitives.
GLfloat yellow[] = {1.0f, 1.0f, 0.0f, 1.0f};
glMaterialfv( GL_FRONT, GL_AMBIENT, yellow );
glMaterialfv( GL_FRONT, GL_DIFFUSE, yellow );

glBegin( GL_TRIANGLES );

The platform is now in a mode in which each trio of calls to
glVertex3f adds one triangle to the mesh.

// Set the current normal vector for the next three vertices.
// Send normalized (unit-length) normal vectors.
glNormal3f( ... );

// Specify the first face’s three vertices.
// Specify vertices of the front side of the face
// in counter-clockwise order, thus explicitly
// identifying which side is front versus back.
glVertex3f(   0.f,  75.f,   0.f );
glVertex3f( -50.f,   0.f,  50.f );
glVertex3f(  50.f,   0.f,  50.f );

// Set the current normal vector for the next three vertices
glNormal3f( ... );

glVertex3f(   0.f,  75.f,   0.f ); // Specify three vertices
glVertex3f(  50.f,   0.f,  50.f );
glVertex3f(  50.f,   0.f, -50.f );

... and so on for the next two faces ...

glEnd(); // Exit the mesh-specification mode

The mesh is now queued for rendering.
```
```

# 16.2.7  Putting It All Together—Part 1: Static Frame

In contrast to WPF, which automatically updates the display to represent the current status of the scene graph, immediate-mode packages place the burden of display refresh on the application. First let’s look at a static-image generator, and then we’ll add dynamics.

Consider the case of a program that is to generate a single static image; in such a case, the rendering activity is only needed

+   - As part of initialization, to generate the first rendering
+   - Whenever the window manager reports to GLUT that the image has been damaged and needs repair (e.g., upon closing of a window that was partially covering the OpenGL window)

In this situation, the display function typically looks like this:

```
```c
void drawEntireScene()
{
    Set up projection transform, as shown above.
    Set up viewing transform, as shown above.
    Draw the scene, via an ordered sequence of actions, such as:
        Set the material state.
        Specify primitive.
```
```