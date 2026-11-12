```
#include "pch.h"
#include "application.h"

namespace fuse {
FUSE_API void run_application(const app_config& config) {
    if(SDL_Init(SDL_INIT_EVERYTHING) == 0) {
        std::cout << "sdl initialized!" << std::endl;
    }
    if(IMG_Init(IMG_INIT_PNG) > 0) {
        std::cout << "sdl image initialized!" << std::endl;
    }
    if(TTF_Init() == 0) {
        std::cout << "sdl ttf initialized!" << std::endl;
    }
    if(Mix_Init(MIX_INIT_MP3) > 0) {
        std::cout << "sdl mixer initialized!" << std::endl;
    }
    SDL_Quit();
    IMG_Quit();
    TTF_Quit();
    Mix_Quit();
}
}
```

To determine whether all the libraries were successfully installed or not, we simply try to initialize each one.

# SDL_Init(Uint32 flags) returns 0 on success or a negative code on failure.

We didn't want to be specific about which system to initialize, so we used the SDL_INIT_EVERYTHING flag to initialize all systems. However, if for instance we only want to initialize audio and video, we can use the OR-operator to combine flags: SDL_Init(SDL_INIT_AUDIO | SDL_INIT_VIDEO).

Note : You can make use of IntelliSense to find out all possible flags.

# IMG_Init(int flags) loads dynamic libraries and prepares them for use. Flags should be one or more flags from IMG_InitFlags OR'd together. It returns the flags successfully initialized, or 0 on failure.

# TTF_Init() Initialize the SDL_ttf engine. Returns 0 if successful, -1 on error.

# Mix_Init(int flags) loads dynamic libraries and prepares them for use. Flags should be one or more flags from MIX_InitFlags OR'd together. It returns the flags successfully initialized, or 0 on failure.