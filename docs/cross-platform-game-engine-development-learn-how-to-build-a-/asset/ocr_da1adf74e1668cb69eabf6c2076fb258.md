```
#include "pch.h"
#include "inputs.h"
#include "ecs/scene.h"
#include "application.h"
#include "events/system.h"

namespace fuse {
static bool is_running = true;
static float deltatime, last_tick;

FUSE_INLINE bool on_quit(const quit_event&) {
    return is_running = false;
}

FUSE_INLINE void compute_deltatime() {
    deltatime = get_ticks() - last_tick;
    if (deltatime > MAX_DELTATIME) {
        deltatime = MAX_DELTATIME;
    }
    last_tick = get_ticks();
}

FUSE_API void run_application(const app_config& config) {
    // ...

    last_tick = get_ticks();

    while (is_running) {
        compute_deltatime();
        inputs::dispatch_events();
        SDL_RenderClear(renderer);
        scene->update(deltatime);
        SDL_RenderPresent(renderer);
    }

    // ...
}
}
```

Add the lines highlighted above in your application.cpp file. As you can see, the function compute_deltatime() will compute the value of the delta for each frame by calculating the difference of time between the current frame and the last frame. To make sure the value of the delta time never gets too high, we always check if