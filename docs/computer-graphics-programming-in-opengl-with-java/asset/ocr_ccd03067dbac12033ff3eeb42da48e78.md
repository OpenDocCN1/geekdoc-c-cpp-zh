includes a vertex and fragment shader. The completed program is placed in the variable “renderingProgram”:

```
renderingProgram = Utils.createShaderProgram("vertShader.glsl", "fragShader.glsl");
```

These createShaderProgram() implementations can all be found on the accompanying CD (in the “Utils.java” file), and all of them incorporate the error-detecting modules from Section 2.2 as well. There is nothing new about them; they are simply organized in this way for convenience. As we move forward in the book, other similar functions will be added to Utils.java as we go along. The reader is strongly encouraged to examine the Utils.java file on the accompanying CD, and even add to it as desired. The programs found there are built from the methods as we learn them in the book, and studying their organization should serve to strengthen one’s own understanding.

![](bbox=[0.87, 0.308, 0.936, 0.358])

Regarding the functions in the “Utils.java” file, we have implemented them as static methods so that it isn’t necessary to instantiate the Utils class. Readers may prefer to implement them as instance methods rather than static methods, depending on the architecture of the particular system being developed.

All of our shader files will be named with a “.glsl” extension.

# SUPPLEMENTAL NOTES

There are many details of the OpenGL pipeline that we have not discussed in this introductory chapter. We have skipped a number of internal stages and have completely omitted how textures are processed. Our goal was to map out, as simply as possible, the framework in which we will be writing our code. As we proceed we will continue to learn additional details.

We have also deferred presenting code examples for tessellation and geometry. In later chapters we will build complete systems that show how to write practical shaders for each of the stages.

There are more sophisticated ways to organize the code for animating a scene, especially with respect to managing threads. Readers interested in designing a render loop (or “game loop”) appropriate for a particular application are encouraged to consult some of the more specialized books on game engine design (e.g., [NY14]), and to peruse the related discussions on gamedev.net [GD21].