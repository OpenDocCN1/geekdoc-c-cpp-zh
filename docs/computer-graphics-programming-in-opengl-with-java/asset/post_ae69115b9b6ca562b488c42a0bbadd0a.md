
Consider, for example, Program 4.1. If we reorganize the code so as to remove the computation of the perspective matrix from display(), then the revised versions of the init(), display(), and reshape() functions would be as follows:

```java
public void init(GLAutoDrawable drawable)
{
    // same as earlier, plus the following two lines:
    aspect = (float) myCanvas.getWidth() / (float) myCanvas.getHeight();
    pMat.setPerspective((float) Math.toRadians(60.0f), aspect, 0.1f, 1000.0f);
}

public void display(GLAutoDrawable drawable)
{
    // same as earlier, except with the following lines removed:
    // build perspective matrix
    // aspect = (float) myCanvas.getWidth() / (float) myCanvas.getHeight();
    // pMat.setPerspective((float) Math.toRadians(60.0f), aspect, 0.1f, 1000.0f);
    // the rest of the function is unchanged
}

public void reshape(GLAutoDrawable drawable, int x, int y, int width, int height)
{
    GL4 gl = (GL4) GLContext.getCurrentGL();
    aspect = (float) width / (float) height;    // new window width & height are provided by the callback
    gl.glViewport(0, 0, width, height);         // sets region of screen associated with the frame buffer
    pMat.setPerspective((float) Math.toRadians(60.0f), aspect, 0.1f, 1000.0f);
}
```

### 4.11.3 Back-Face Culling

Another way of improving rendering efficiency is to take advantage of OpenGL’s ability to do *back-face culling*. When a 3D model is entirely “closed,” meaning the interior is never visible (such as for the cube and for the pyramid), then it turns out that those portions of the outer surface that are angled away from the viewer will always be obscured by some other portion of the same model. That is, those triangles that face away from the viewer cannot possibly be seen (they would be overwritten by hidden surface removal anyway), and thus there is no reason to rasterize or render them.

We can ask OpenGL to identify and “cull” (not render) back-facing triangles with the command glEnable(GL_CULL_FACE). We can also disable face culling with glDisable(GL_CULL_FACE). By default, face culling is disabled, so if you want OpenGL to cull back-facing triangles, you must enable it.

When face culling is enabled, by default triangles are rendered only if they are *front-facing*. Also by default a triangle is considered front-facing if its three vertices progress in a *counterclockwise* direction (based on the order that they were defined in the buffer) as viewed from the OpenGL camera. Triangles whose vertices progress in a clockwise direction (as viewed from the OpenGL camera) are *back-facing*, and are not rendered. This counterclockwise definition of “front-facing” is sometimes called the *winding order*, and can be set explicitly using the function call glFrontFace(GL_CCW) for counterclockwise (the default) or glFrontFace(GL_CW) for clockwise. Similarly, whether it is the front-facing or the back-facing triangles that are rendered can also be set explicitly. Actually, for this purpose we specify which ones are *not* to be rendered—that is, which ones are “culled.” We can specify that the back-facing triangles be culled (although this would be unnecessary because it is the default) by calling glCullFace(GL_BACK). Alternatively, we can specify instead that the front-facing triangles be culled, or even that all of the triangles be culled, by replacing the parameter GL_BACK with either GL_FRONT or GL_FRONT_AND_BACK, respectively.

As we will see in Chapter 6, 3D models are typically designed so that the outer surface is constructed of triangles with the same winding order—most commonly counterclockwise—so that if culling is enabled, then by default the portion of the model’s outer surface that faces the camera is rendered. Since by default OpenGL assumes the winding order is counterclockwise, if a model is designed to be displayed with a *clockwise* winding order, it is up to the programmer to call glFrontFace(GL_CW) to account for this if back-face culling is enabled.

Note that in the case of GL_TRIANGLE_STRIP, the winding order of each triangle alternates. OpenGL compensates for this by “flipping” the vertex sequence when building each successive triangle, as follows: 0-1-2, then 2-1-3, 2-3-4, 4-3-5, 4-5-6, and so on.

Back-face culling improves performance by ensuring that OpenGL doesn’t spend time rasterizing and rendering surfaces that are never intended to be seen. Most of the examples we have seen in this chapter are so small that there is little motivation to enable face culling (an exception is the example shown in Figure 4.9, with the 100,000 instanced animated cubes, which may pose a performance challenge on some systems). In practice, it is common for most 3D models to be “closed,” and so it is customary to routinely enable back-face culling. For example, we can add back-face culling to Program 4.3 by modifying the display() function as follows:

```java
public void display(GLAutoDrawable drawable)
{
  . . .
  gl.glEnable(GL_CULL_FACE);

  // draw the cube

  gl.glEnable(GL_DEPTH_TEST);
  gl.glDepthFunc(GL_LEQUAL);
  gl.glFrontFace(GL_CW);         // the cube vertices have clockwise winding order
  gl.glDrawArrays(GL_TRIANGLES, 0, 36);

  // draw the pyramid

  . . .
  gl.glEnable(GL_DEPTH_TEST);
  gl.glDepthFunc(GL_LEQUAL);
  gl.glFrontFace(GL_CCW);        // the pyramid vertices have counter-clockwise winding order
  gl.glDrawArrays(GL_TRIANGLES, 0, 18);
}
```

Properly setting the winding order is important when using back-face culling. An incorrect setting, such as GL_CW when it should be GL_CCW, can lead to the interior of an object being rendered rather than its exterior, which in turn can produce distortion similar to that of an incorrect perspective matrix.

Efficiency isn't the only reason for doing face culling. In later chapters we will see other uses, such as for those circumstances when we want to see the *inside* of a 3D model or when using transparency.

## SUPPLEMENTAL NOTES

JOML has a huge variety of functions for performing translation, rotation, and scaling. For example, JOML's functions "translate()" and "translation()" are slightly different. The first concatenates a translation onto an existing matrix, whereas the second builds a translation matrix. We have used both of these functions in our examples, and there are many others to choose from. The reader should be careful to double-check that the JOML function being used does exactly what is desired.

As mentioned in this chapter, when using Java buffers it is advisable to ensure that only direct buffers are used. For example, it is tempting to use the Java FloatBuffer.wrap() function to put vertex data stored in an array into a buffer. However, wrap() produces a *non-direct* buffer, in which the resulting buffer is a wrapper for data that is still stored in an array.⁶ One approach for copying the data into a *direct* buffer is to allocate a direct ByteBuffer, use ByteBuffer.asFloatBuffer() to view it as a FloatBuffer, and then use a loop with the put() command to copy the data one at a time. As described earlier, the JOGL com.jogamp.common.nio.Buffers class makes it easier to populate direct buffers by providing convenience methods for loading array data into a variety of buffer types:

- `newDirectByteBuffer(byte[ ])`
- `newDirectCharBuffer(char[ ])`
- `newDirectDoubleBuffer(double[ ])`
- `newDirectFloatBuffer(float[ ])`
- `newDirectIntBuffer(int[ ])`
- `newDirectLongBuffer(long[ ])`
- `newDirectShortBuffer(short[ ])`

Using the above JOGL methods for populating buffers with vertex data (that is, data intended to be used by JOGL applications) also ensures correct native byte ordering. It also ensures correct size allocation and makes an explicit allocation unnecessary.

There is a myriad of other capabilities and structures available for managing and utilizing data in OpenGL/JOGL/GLSL, and we have only scratched the surface in this chapter. We haven’t, for example, described a *uniform block*, which is a mechanism for organizing uniform variables similar to a *struct* in C. Uniform blocks can even be set up to receive data from buffers. Another powerful mechanism is a *shader storage block*, which is essentially a buffer into which a shader can write.

An excellent reference on the many options for managing data (albeit in C++) is the *OpenGL SuperBible* [SW15], particularly the chapter entitled “Data” (Chapter 5 in the seventh edition). It also describes many of the details and options

⁶ Using non-direct buffers is actually allowable in JOGL. However, when a non-direct buffer is passed to a JOGL method, JOGL will convert it to a direct buffer, and this conversion incurs a performance penalty.
