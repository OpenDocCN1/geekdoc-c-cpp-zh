# Figure 17.8

Controlling scene parameters with a separate controller pane — one of many possible ways to control an OpenGL scene.

![](bbox=[0.214, 0.24, 0.789, 0.468])

As an exercise, you can try to improve the project. In this version, the timer animation stops when the user moves a slider. To move the timer and the drawRect: method to a sub-thread so that they run independently of the UI. Chapter 11 has some hints about thread management.

You can also create a more sophisticated OpenGL view by adding extra lights, customizing the texture, and improving the depth culling that controls the order in which the visible surfaces are drawn.

> **TIP**
> 
> A useful series of unofficial tutorials is available at http://nehe.gamedev.net. The Cocoa versions of the projects are out of date now, but you can extract the code from the Web site examples and copy it into the OpenGL project sample code. Official documentation is available at www.opengl.org.