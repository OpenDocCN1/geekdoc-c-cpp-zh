acceleration. This means that the OpenGL rendering will run on graphics hardware (a GPU).

# The OpenGL Context and Initializing GLEW

Once the OpenGL attributes are set and you've created the window, the next step is to create an OpenGL context. Think of a **context** as the “world” of OpenGL that contains every item that OpenGL knows about, such as the color buffer, any images or models loaded, and any other OpenGL objects. (While it is possible to have multiple contexts in one OpenGL program, this book sticks to one.)

To create the context, first add the following member variable to `Game`:

```
SDL_GLContext mContext;
```

Next, immediately after creating the SDL window with `SDL_CreateWindow`, add the following line of code, which creates an OpenGL context and saves it in the member variable:

> Click here to view code image

```
mContext = SDL_GL_CreateContext(mWindow);
```

As with creating and deleting the window, you need to delete the OpenGL context in the destructor. To do this,