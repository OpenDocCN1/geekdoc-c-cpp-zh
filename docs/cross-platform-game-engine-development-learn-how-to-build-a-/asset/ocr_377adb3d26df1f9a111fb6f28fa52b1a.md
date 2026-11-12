```
#include "pch.h"
#include "inputs.h"
#include "application.h"
#include "events/system.h"

namespace fuse {
static bool is_running = true;

FUSE_INLINE bool on_quit(const quit_event&) {
    return is_running = false;
}

FUSE_API void run_application(const app_config& config) {
    // ...
    inputs::initialize(window);
    inputs::get_dispatcher()->add_callback<quit_event>(on_quit);

    while (is_running) {
        inputs::dispatch_events();
        SDL_RenderClear(renderer);
        SDL_RenderPresent(renderer);
    }
}
}
```

We define a callback-function, on_quit() which simply changes the value of the is-running boolean to “false” when the window’s close button is clicked. This causes our game loop to stop its cycle. We use the dispatcher to register the function-callback. If we were in a class, we would register the function as below.

```
get_dispatcher()->add_callback<quit_event>(ORBIT_BIND(on_quit));
```

We would have needed our ORBIT_BIND macros to be able to register a member function of a class.

# More Events

Now that the foundation is established, we will use the same principle to add more events like mouse down, mouse up, and mouse scroll. The following code snippet shows a list of custom events.

+   engine/src/events/system.h