To use SDL's graphics code, you need to construct an SDL_Renderer via the SDL_CreateRenderer function. The term renderer generically refers to any system that draws graphics, whether 2D or 3D. Because you need to reference this SDL_Renderer object every time you draw something, first add an mRenderer member variable to Game:

```
SDL_Renderer* mRenderer;
```

Next, in Game::Initialize, after creating the window, create the renderer:

Click here to view code image

```
mRenderer = SDL_CreateRenderer(
    mWindow, // Window to create renderer for
    -1,      // Usually -1
    SDL_RENDERER_ACCELERATED | SDL_RENDERER_PRESENTVSY
);
```

The first parameter to SDL_CreateRenderer is the pointer to the window (which you saved in mWindow). The second parameter specifies which graphics driver to use; this might be relevant if the game has multiple windows. But with only a single window, the default is -1, which means to let SDL decide. As with the other