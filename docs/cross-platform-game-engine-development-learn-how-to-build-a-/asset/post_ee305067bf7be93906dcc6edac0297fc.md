
```cpp
#include "pch.h"
#include "inputs.h"
#include "ecs/scene.h"
#include "application.h"
#include "events/system.h"
```

```cpp
namespace fuse {
static app_config config;
static bool is_running = true;
static ecs::scene* scene = NULL;
static float deltatime, last_tick;
}
```

```cpp
FUSE_INLINE bool on_quit(const quit_event&) {
    return is_running = false;
}
```

```cpp
FUSE_INLINE bool on_key(const keydown_event& e) {
    if (e.key == SDL_SCANCODE_R) {
        scene->deserialize(config.scene);
    }
    return false;
}
```

```cpp
FUSE_INLINE void compute_deltatime() {
    deltatime = get_ticks() - last_tick;
    if (deltatime > MAX_DELTATIME) {
        deltatime = MAX_DELTATIME;
    }
    last_tick = get_ticks();
}
```

```cpp
FUSE_API void run_application(const app_config& cfg) {
    // set config
    config = cfg;

    // init SDL
    if (SDL_Init(SDL_INIT_EVERYTHING) < 0) {
        FUSE_ERROR("%s", SDL_GetError());
        exit(EXIT_FAILURE);
    }

    // init SDL_image
    if (IMG_Init(IMG_INIT_JPG | IMG_INIT_PNG) < 0) {
        FUSE_ERROR("%s", IMG_GetError());
    }

    // init SDL_ttf
    if (TTF_Init() < 0) {
        FUSE_ERROR("%s", TTF_GetError());
    }

    // init SDL_mixer
    if (Mix_Init(MIX_INIT_MP3 | MIX_INIT_OGG) < 0 ||
        Mix_OpenAudio(44100, MIX_DEFAULT_FORMAT, 2, 512)) {
        FUSE_ERROR("%s", Mix_GetError());
    }

    // create window
    auto w_flags = (SDL_WindowFlags)(SDL_WINDOW_RESIZABLE |
        SDL_WINDOW_ALLOW_HIGHDPI);
    SDL_Window* window = SDL_CreateWindow(config.title.c_str(),
        SDL_WINDOWPOS_CENTERED,
        SDL_WINDOWPOS_CENTERED, config.width, config.height,
        w_flags);

    // create renderer
    auto r_flags = (SDL_RendererFlags)(SDL_RENDERER_ACCELERATED |
        SDL_RENDERER_PRESENTVSYNC);
    auto renderer = SDL_CreateRenderer(window, -1, r_flags);
    if (!window || !renderer) {
        FUSE_ERROR("%s", SDL_GetError());
        exit(EXIT_FAILURE);
    }

    // register callbacks
    inputs::initialize(window);
    auto di_sp = inputs::get_dispatcher();
    di_sp->add_callback<quit_event>(on_quit);
    di_sp->add_callback<keydown_event>(on_key);

    // create & start scene
    scene = new ecs::scene(renderer);
    scene->deserialize(config.scene);

    last_tick = get_ticks();

    while (is_running) {
        compute_deltatime();
        inputs::dispatch_events();
        SDL_RenderClear(renderer);
        scene->update(deltatime);
        SDL_RenderPresent(renderer);
    }

    // free memory
    SDL_DestroyRenderer(renderer);
    SDL_DestroyWindow(window);
    FUSE_DELETE(scene);
    IMG_Quit();
    Mix_Quit();
    TTF_Quit();
    SDL_Quit();
}
```

We have highlighted all the changes made in the application.cpp so that you can quickly see what is important for you. We have moved the scene definition outside of the run_application function to allow the key down event callback to access the scene deserialize function. The game will restart when the key “R” is pressed.

We have also added a definition for the application config so that we could always access the scene path whenever the game is reloaded.
If you compile your project and run it, you will be able to reload the game by just pressing the key “R”.

![](img/2763810ed0a1572c2bec59ee52dd75be_264_0.png)

# Summary

We were able to serialize and deserialize our game successfully. I hope you’re having as much fun as I am right now. We haven’t written functions to de- and serialize the tile map asset, tile map component, and tile component, but I’m certain you can do it yourself.

Feel free to experience with yaml-cpp to add more features to your project.

Note: You can get the source code from the GitHub repository. The name of the branch that holds the current state of the code is called: “serialization”.

# Chapter 15

Conclusion

# Conclusion

There are many things you can do to make your game engine more valuable. One of them is to add more features.

# Potential Features

Here are some additional features that you could add to your engine

# Scene Editor

You can add a scene editor to your engine to make game development easier. There are many C++ GUI libraries available, but "Dear ImGui" is one that I would strongly recommend.

![](img/2763810ed0a1572c2bec59ee52dd75be_267_0.png)

Figure 52 Example Scene Editor

# Runtime Scripting

Runtime scripting allows game engines like Unity and Unreal Engine to quickly create game behavior without having to recompile the entire engine every time the script code is changed.

Python is a language that is relatively simple to learn and use. However, you can look into scripting with C# and other languages.

# Joysticks Control

I would recommend that you look into the ability to play games using joysticks. Joystick inputs can be handled using SDL's built-in event for joysticks.

# Perspectives

My hope is that you now have a better understanding of the subject discussed in this book. Because the goal of this book was to alleviate the feeling of not knowing or not being certain about your knowledge of the subject. I am confident in stating that the foundation we have established in this book is a strong one for software architecture in general. This knowledge can be applied to any aspect of software development.

Best wishes to you as you embark on this new chapter of your journey as a developer. May God bless you and keep you healthy.

# References

- 2021. Box2D: Overview. https://box2d.org/documentation/. Accessed 18 January 2022.
- 2022. Documentation for Visual Studio Code. https://code.visualstudio.com/docs. Accessed 28 January 2022.
- 2022. Friend declaration - cppreference.com. https://en.cppreference.com/w/cpp/language/friend. Accessed 15 February 2022.
- 2022. Function template - cppreference.com. https://en.cppreference.com/w/cpp/language/function_template. Accessed 1 October 2022.
- GitHub. 2022. jbeder/yaml-cpp: A YAML parser and emitter in C++. https://github.com/jbeder/yaml-cpp. Accessed 14 February 2022.
- GitHub. 2022. libcyaml/guide.md at main · tlsal/libcyaml. https://github.com/tlsal/libcyaml. Accessed 14 February 2022.
- GitHub. 2022. libfyaml/libfyaml.h at master · pantoniou/libfyaml. https://github.com/pantoniou/libfyaml. Accessed 14 February 2022.
- GitHub. 2022. yaml/libyaml: Canonical source repository for LibYAML. https://github.com/yaml/libyaml. Accessed 14 February 2022.
- GitHub. 2022. SanderMertens/ecs-faq: Frequently asked questions about Entity Component Systems. https://github.com/SanderMertens/ecs-faq. Accessed 1 November 2022.
- 2019. How to Create a Random Number Generator in C++. BitDegree (Oct. 2019).
- 2022. How to Install libyaml-cpp-dev in Ubuntu 18.04. https://www.howtoinstall.me/ubuntu/18-04/libyaml-cpp-dev/. Accessed 14 February 2022.
- 2019. https://www.libsdl.org/projects/SDL_image. https://www.libsdl.org/projects/SDL_image/. Accessed 1 July 2022.
- 2018. https://www.libsdl.org/projects/SDL_mixer. https://www.libsdl.org/projects/SDL_mixer/. Accessed 1 July 2022.
- 2018. https://www.libsdl.org/projects/SDL_ttf#source. https://www.libsdl.org/projects/SDL_ttf/. Accessed 1 July 2022.
- Isaac Physics. 2022. Isaac Physics. https://isaacphysics.org/concepts/cp_friction?stage=all. Accessed 18 January 2022.
- Rungta, K. 2020. Entity Component System. Guru99 (Jul. 2020).
- 2013. SDL_ttf 2.0.7: TTF_SetFontStyle. https://www.libsdl.org/projects/docs/SDL_ttf/SDL_ttf_22.html. Accessed 14 January 2022.
- 2022. Simple DirectMedia Layer - Homepage. https://www.libsdl.org/. Accessed 1 July 2022.
- 2021. The Official YAML Web Site. https://yaml.org/. Accessed 14 February 2022.
- 2022. Tiles and tilemaps overview - Game development | MDN. https://developer.mozilla.org/en-US/docs/Games/Techniques/Tilemaps. Accessed 16 January 2022.
- [1] Wikipedia. 2021. Acceleration. https://en.wikipedia.org/w/index.php?title=Acceleration&oldid=1062249960. Accessed 18 January 2022.
- [2] Wikipedia. 2021. Delta Time. https://de.wikipedia.org/w/index.php?title=Delta_Time&oldid=216945978. Accessed 18 January 2022.
- [3] Wikipedia. 2021. Flappy Bird. https://de.wikipedia.org/w/index.php?title=Flappy_Bird&oldid=215855578. Accessed 2 September 2022.
- [4] Wikipedia. 2021. Tile-based video game. https://en.wikipedia.org/w/index.php?title=Tile-based_video_game&oldid=1059809510. Accessed 16 January 2022.
- [5] Wikipedia. 2021. TrueType. https://de.wikipedia.org/w/index.php?title=TrueType&oldid=217573606. Accessed 1 December 2022.
- [6] Wikipedia. 2022. Scripting language. https://en.wikipedia.org/w/index.php?title=Scripting_language&oldid=1066860674. Accessed 21 January 2022.
- [7] Wikipedia. 2022. Serialization. https://en.wikipedia.org/w/index.php?title=Serialization&oldid=1071395024. Accessed 14 February 2022.
- [8] Wikipedia. 2022. Velocity. https://en.wikipedia.org/w/index.php?title=Velocity&oldid=1063300750. Accessed 18 January 2022.
- [9] Wikipedia. 2022. YAML. https://en.wikipedia.org/w/index.php?title=YAML&oldid=1070505919. Accessed 14 February 2022.
