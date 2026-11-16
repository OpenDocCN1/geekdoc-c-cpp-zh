```
// Now create a shader program that
// links together the vertex/frag shaders
mShaderProgram = glCreateProgram();
glAttachShader(mShaderProgram, mVertexShader);
glAttachShader(mShaderProgram, mFragShader);
glLinkProgram(mShaderProgram);

// Verify that the program linked successfully
if (!IsValidProgram())
{
    return false;
}
return true;
}
```

After you've compiled both the fragment and vertex shader, you link them together in a third object, called a shader program. When it's time to draw an object, OpenGL uses the currently active shader program to render the triangles.

You create a shader program with glCreateProgram,