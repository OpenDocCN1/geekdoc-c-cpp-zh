If the timer ticks more than 25 times a second, the scene animation appears smooth. In this example, you use the timer to update a variable that defines the rotation of the scene.

An OpenGL scene is defined by a long list of functions. Typically the code does the following:

+   1. Initializes lights and materials
+   2. Defines the viewport and camera position
+   3. Places objects in the scene
+   4. Calls `glFinish()` to render the scene

The `glFinish()` function compiles the scene code and runs it, creating the finished view. Sample code for the teapot example is as follows. The code uses the OpenGL and GLUT libraries, so you must add these to your project, with their headers.

```
```objective-c
- (void) timerMethod {
    //Increment the rotation value, and refresh the display
    rotationCount +=rotationStep;
    [self setNeedsDisplay: YES];
}

- (void)drawRect:(NSRect)dirtyRect {
    //Setup a context
    NSOpenGLContext *glContext = [self openGLContext];
    [glContext makeCurrentContext];
    //Basic setup
    glEnable(GL_LIGHTING);
    glEnable(GL_DEPTH_TEST);
    glDepthFunc(GL_LEQUAL);
    glClearDepth(1.0);
    glEnable(GL_CULL_FACE);

    //Ambient light
    GLfloat ambientLight[] = {ambientBrightness,
    ambientBrightness, ambientBrightness, 1.0};
    glLightModelfv(GL_LIGHT_MODEL_AMBIENT, ambientLight);
    //Add a diffuse white light
    GLfloat diffuseLight[] = {diffuseBrightness,
    diffuseBrightness, diffuseBrightness, 1.0};
    glLightfv(GL_LIGHT0, GL_DIFFUSE, diffuseLight);
    //Some specular highlights, same value as the diffuse light
    GLfloat specularLight[] = {diffuseBrightness,
    diffuseBrightness, diffuseBrightness, 1.0};
    glLightfv(GL_LIGHT0, GL_SPECULAR, specularLight);
    //Turn on the light
    glEnable(GL_LIGHT0);
```

```