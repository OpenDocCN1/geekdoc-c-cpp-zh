```
gl.glProgramUniform1f(renderingProgram, offsetLoc, x); // send value in "x" to "offset"
gl.glDrawArrays(GL_TRIANGLES, 0, 3);
} ... // remaining functions, same as before
}
```

Vertex shader:

```
#version 430
uniform float offset;
void main(void)
{ if (gl_VertexID == 0) gl_Position = vec4( 0.25 + offset, -0.25, 0.0, 1.0);
  else if (gl_VertexID == 1) gl_Position = vec4(0.25 + offset, -0.25, 0.0, 1.0);
  else gl_Position = vec4( 0.25 + offset,  0.25, 0.0, 1.0);
}
```

Note that in addition to adding code to animate the triangle, we have also added the following line at the beginning of the display() function:

```
gl.glClear(GL_DEPTH_BUFFER_BIT);
```

While not strictly necessary in this particular example, we have added it here and it will continue to appear in most of our applications. Recall from the discussion in Section 2.1.7 that hidden surface removal requires both a color buffer and a depth buffer. As we proceed to drawing progressively more complex 3D scenes, it will be necessary to initialize (clear) the depth buffer each frame, especially for scenes that are animated, to ensure that depth comparisons aren't affected by old depth data. It should be apparent from the example above that the command for clearing the depth buffer is essentially the same as for clearing the color buffer.

![](bbox=[0.52, 0.35, 0.88, 0.88])