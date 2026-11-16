
add the following line of code to Game::Shutdown, right before the call to SDL_DeleteWindow:

Click here to view code image

```
SDL_GL_DeleteContext(mContext);
```

Although the program now creates an OpenGL context, there is one final hurdle you must pass to gain access to the full set of OpenGL 3.3 features. OpenGL supports backward compatibility with an extension system. Normally, you must query any extensions you want manually, which is tedious. To simplify this process, you can use an open source library called the OpenGL Extension Wrangler Library (GLEW). With one simple function call, GLEW automatically initializes all extension functions supported by the current OpenGL context’s version. So in this case, GLEW initializes all extension functions supported by OpenGL 3.3 and earlier.

To initialize GLEW, you add the following code immediately after creating the OpenGL context:

Click here to view code image

```
// Initialize GLEW

glewExperimental = GL_TRUE;
if (glewInit() != GLEW_OK)
{
    SDL_Log("Failed to initialize GLEW.");

    return false;
}

// On some platforms, GLEW will emit a benign error code
// so clear it

glGetError();
```

The glewExperimental line prevents an initialization error that may occur when using the core context on some platforms. Furthermore, because some platforms emit a benign error code when initializing GLEW, the call to glGetError clears this error code.

Note: Some old PC machines with integrated graphics (from 2012 or earlier) may have issues running OpenGL version 3.3. In this case, you can try two things: updating to newer graphics drivers or requesting OpenGL version 3.1.

## Rendering a Frame

You now need to convert the clear, draw scene, and swap buffers process in Game::GenerateOutput to use OpenGL functions:

Click here to view code image

```
// Set the clear color to gray

glClearColor(0.86f, 0.86f, 0.86f, 1.0f);

// Clear the color buffer
glClear(GL_COLOR_BUFFER_BIT);

// TODO: Draw the scene

// Swap the buffers, which also displays the scene
SDL_GL_SwapWindow(mWindow);
```

This code first sets the clear color to 86% red, 86% green, 86% blue, and 100% alpha, which yields a gray color. The `glClear` call with the `GL_COLOR_BUFFER_BIT` parameter clears the color buffer to the specified color. Finally, the `SDL_GL_SwapWindow` call swaps the front buffer and back buffer. At this point, running the game yields a gray screen because you aren’t drawing the `SpriteComponent`s yet.

## TRIANGLE BASICS

The graphical needs of 2D and 3D games couldn’t seem more different. As discussed in Chapter 2, “Game Objects and 2D Graphics,” most 2D games use sprites for their 2D characters. On the other hand, a 3D game features a simulated 3D environment that you somehow flatten into a 2D image that you show onscreen.

Early 2D games could simply copy sprite images into the desired locations of the color buffer. This process, called **blitting**, was efficient on sprite-based consoles such as the Nintendo Entertainment System (NES). However, modern graphical hardware is inefficient at blitting but is very efficient at polygonal rendering. Because of this, nearly all modern games, whether 2D or 3D, ultimately use polygons for their graphical needs.

## Why Polygons?

There are many ways a computer could simulate a 3D environment. Polygons are popular in games for a multitude of reasons. Compared to other 3D graphics techniques, polygons do not require as many calculations at runtime. Furthermore, polygons are scalable: A game running on less-powerful hardware could simply use 3D models with fewer polygons. And, importantly, you can represent most 3D objects with polygons.

Triangles are the polygon of choice for most games. Triangles are the simplest polygon, and you need only three points (or **vertices**) to create a triangle. Furthermore, a triangle can only lie on a single plane. In other words, the three points of a triangle must be **coplanar**. Finally, triangles **tessellate** easily, meaning it's relatively simple to break any complex 3D object into many triangles. The remainder of this chapter talks about triangles, but the techniques discussed here also work for other polygons (such as quads), provided that they maintain the coplanar property.

2D games use triangles to represent sprites by drawing a rectangle and filling in the rectangle with colors from an image file. We discuss this in much greater detail later in the chapter.

## Normalized Device Coordinates

To draw a triangle, you must specify the coordinates of its three vertices. Recall that in SDL, the top-left corner of the screen is (0, 0), positive x is to the right, and positive y is down. More generally, a **coordinate space** specifies where the origin is and in which direction its coordinates increase. The **basis vectors** of the coordinate space are the direction in which the coordinates increase.

An example of a coordinate space from basic geometry is a **Cartesian coordinate system** (see Figure 5.1). In a 2D Cartesian coordinate system, the origin (0, 0) has a specific point (usually the center), positive x is to the right, and positive y is up.

![](img/e9afcec1487716b0ef80d7e7c09869c8_314_0.png)

Figure 5.1 A point drawn at (2, 3) in a Cartesian coordinate system

**Normalized device coordinates (NDC)** is the default coordinate system used with OpenGL. Given an OpenGL window, the center of the window is the origin in normalized device coordinates. Furthermore, the bottom-left corner is (-1, -1), and the top-right corner is (1, 1). This is regardless of the width and height of the window (hence *normalized device coordinates*). Internally, the graphics hardware then converts these NDC into the corresponding pixels in the window.

For example, to draw a square with sides of unit length in the center of the window, you need two triangles. The first triangle has the vertices (-0.5, 0.5), (0.5, 0.5), and (0.5, -0.5), and the second triangle has the vertices (0.5, -0.5), (-0.5, -0.5), and (-0.5, 0.5). Figure 5.2 illustrates this square. Keep in mind that if the length and width of the window are not uniform, a square in normalized device coordinates will not look like a square onscreen.

![](img/e9afcec1487716b0ef80d7e7c09869c8_315_0.png)

Figure 5.2 A square drawn in 2D normalized device coordinates

In 3D, the z component of normalized device coordinates also ranges from [-1, 1], with a positive z value going into the screen. For now, we stick with a z value of zero. We’ll explore 3D in much greater detail in Chapter 6, “3D Graphics.”

## Vertex and Index Buffers

Suppose you have a 3D model comprised of many triangles. You need some way to store the vertices of these triangles in memory. The simplest approach is to directly store the coordinates of each triangle in a contiguous array or buffer. For example, assuming 3D coordinates, the following array contains the vertices of the two triangles shown in Figure 5.2:

```
float vertices[] = {
    -0.5f,  0.5f, 0.0f,
    0.5f,  0.5f, 0.0f,
    0.5f, -0.5f, 0.0f,
    0.5f, -0.5f, 0.0f,
    -0.5f, -0.5f, 0.0f,
    -0.5f,  0.5f, 0.0f,
};
```

Even in this simple example, the array of vertices has some duplicate data. Specifically, the coordinates (-0.5, 0.5, 0.0) and (0.5, -0.5, 0.0) appear twice. If there were a way to remove these duplicates, you would cut the number of values stored in the buffer by 33%. Rather than having 12 values, you would have only 8. Assuming single-precision floats that use 4 bytes each, you'd save 24 bytes of memory by removing the duplicates. This might seem insignificant, but imagine a much larger model with 20,000 triangles. In this case, the amount of memory wasted due to duplicate coordinates would be high.

The solution to this issue has two parts. First, you create a vertex buffer that contains only the unique coordinates used by the 3D geometry. Then, to specify
