| SDL_INIT_AUDIO | Audio device management, playback, and recording |
| SDL_INIT_VIDEO | Video subsystem for creating a window, interfacing with OpenGL, and 2D graphics |
| SDL_INIT_HAPTIC | Force feedback subsystem |
| SDL_INIT_GAMECONTROLLER | Subsystem for supporting controller input devices |

If SDL initializes successfully, the next step is to create a window with the `SDL_CreateWindow` function. This is just like the window that any other Windows or macOS program uses. The `SDL_CreateWindow` function takes in several parameters: the title of the window, the x/y coordinates of the top-left corner, the width/height of the window, and optionally any window creation flags:

Click here to view code image

```
mWindow = SDL_CreateWindow(
    "Game Programming in C++ (Chapter 1)", // Window title
    100, // Top left x-coordinate of window
    100, // Top left y-coordinate of window
    1024, // Width of window
    768, // Height of window
    0 // Flags (0 for no flags set)
)
```