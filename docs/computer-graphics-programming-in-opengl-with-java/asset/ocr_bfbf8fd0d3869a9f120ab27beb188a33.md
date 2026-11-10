entire stack is allocated ahead of time, so the “push” operations done in display() don’t allocate space dynamically. In fact, we now minimize the number of declarations or instantiations of any kind that appear in display(). For example, Program 4.1 included the following block of code early in its listing:

```
    // allocate variables used in display(), so they aren't allocated during rendering
    private FloatBuffer vals = Buffers.newDirectFloatBuffer(16);   // for transferring matrices
    private Matrix4f pMat = new Matrix4f();    // perspective matrix
    private Matrix4f vMat = new Matrix4f();    // view matrix
    private Matrix4f mMat = new Matrix4f();    // model matrix
    private Matrix4f mvMat = new Matrix4f();   // model-view matrix
    private int mvLoc, pLoc;
    private float aspect;
```

Note that we purposely placed a comment at the top of the block indicating that these variables are pre-allocated for later use in the display() function (although we are only explicitly pointing that out now).

There are other, more subtle examples. For example, function calls that convert data from one type to another may in some cases instantiate and return the newly converted data. It is thus important to understand the behaviors of any library functions called from display().

Fortunately, the math library we are using, JOML, has been carefully designed to eliminate (or at least minimize) memory allocation as a result of calling its functions, while still providing needed capabilities for OpenGL. Most of its functions operate directly on the object from which the function is invoked, or on one of its parameters (rather than building an answer and returning it), and thus in either case allowing for the space holding the result to be pre-allocated.

An example of how cleverly JOML was designed to maximize performance in this way is seen in the calls to glUniformMatrix4fv(). Let’s take a closer look at one such call, that transfers the model-view matrix to a uniform variable:

```
    gl.glUniformMatrix4fv(mvLoc, 1, false, mvMat.get(vals));
```

Recall that the variable mvMat is of type Matrix4f, and that we wish to send the values in that matrix to the shader uniform pointed to by mvLoc. As expected,