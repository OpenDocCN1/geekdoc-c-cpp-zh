```
// For now, just a position.
in vec3 inPosition;

void main()
{
    // Directly pass along inPosition to gl_Position
    gl_Position = vec4(inPosition, 1.0);
}
```

# The Basic.frag File

The job of the fragment shader is to compute an output color for the current pixel. For Basic.frag, you'll hard-code a blue output color for all pixels.

As with the vertex shader, the fragment shader always begin with a #version line. Next, you declare a global variable to store the output color, using the out variable specifier:

```
out vec4 outColor;
```

The outColor variable is a vec4 corresponding to the four components of the RGBA color buffer.

Next, you declare the entry point of the fragment shader program. Inside this function, you set outColor to the