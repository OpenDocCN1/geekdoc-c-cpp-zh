# ### Program 15.7 — Animating the Water's Surface

C++/OpenGL Application

```
~~~cpp
...
float depthLookup = 0.0f;
GLuint dOffsetLoc;

double turbulence(double x, double y, double z, double maxZoom) {
    double sum = 0.0, zoom = maxZoom;
    sum = sin((1.0/512.0)*(PI*x*z*4.0)) + 1.0;  //this change moves the sine wave through the noise map
    ...
}

void prepForTopSurfaceRenderer() {
    ...
    dOffsetLoc = glGetUniformLocation(renderingProgramSURFACE, "depthOffset");
    glUniform1f(dOffsetLoc, depthLookup);
    ...
}

void prepForFloorRenderer() {
    ...
    dOffsetLoc = glGetUniformLocation(renderingProgramFLOOR, "depthOffset");
    glUniform1f(dOffsetLoc, depthLookup);
    ...
}

void display(GLFWwindow* window, double currentTime) {
    depthLookup += (currentTime - prevTime) * 0.05f;
    prevTime = currentTime;    // prevTime is a global variable initialized to glfwGetTime() in init()
    ...
}
~~~
```

*Vertex Shaders (for top surface, and for floor)*

```
~~~cpp
...
uniform float depthOffset;
...
~~~
```

*Fragment Shaders (for top surface, and for floor)*

```
~~~cpp
...
uniform float depthOffset;
vec3 estimateWaveNormal(float offset, float mapScale, float hScale)
{
    ...
}
~~~
```