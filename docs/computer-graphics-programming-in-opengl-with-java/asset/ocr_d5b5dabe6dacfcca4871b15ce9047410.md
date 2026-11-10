shader simply output a particular color—solid blue, for example. If the subsequent output is of the correct geometric form (but solid blue), the vertex shader is probably correct, and there is an error in the original fragment shader. If the output is still a blank screen, the error is more likely earlier in the pipeline, such as in the vertex shader.

In Appendix C we show how to use yet another useful debugging tool called *Nsight*, which is available for machines equipped with certain Nvidia graphics cards.

# ## 2.3 READING GLSL SOURCE CODE FROM FILES

So far, our GLSL shader code has been stored inline in strings. As our programs grow in complexity, this will become impractical. We should instead store our shader code in files and read them in.

Reading text files is a basic Java skill, and won’t be covered here. However, for practicality, code to read shaders is provided in `readShaderSource()`, shown in Program 2.4. It reads the shader text file and returns an array of strings, where each string is one line of text from the file. It then determines the size of that array based on how many lines were read in. Note that here, `createShaderProgram()` replaces the version from Program 2.2.

In this example, the vertex and fragment shader code is now placed in the text files “vertShader.glsl” and “fragShader.glsl,” respectively.

# ### Program 2.4 Reading GLSL Source from Files

```
    (...imports as before, plus the following...)
    import java.io.File;
    import java.io.IOException;
    import java.util.Scanner;

    public class Code extends JFrame implements GLEventListener
    {  (... declarations same as before, display() as before)
        private int createShaderProgram()
        {  (... as before plus...)
            vshaderSource = readShaderSource("vertShader.glsl");
            fshaderSource = readShaderSource("fragShader.glsl");

            gl.glShaderSource(vertexShader, vshaderSource.length, vshaderSource, null, 0);
            gl.glShaderSource(fragmentShader, fshaderSource.length, fshaderSource, null, 0);
```