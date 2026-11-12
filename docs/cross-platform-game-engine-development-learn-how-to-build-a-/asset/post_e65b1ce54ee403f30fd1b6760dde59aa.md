
template argument for the type of the event to post with all the parameters necessary to construct that event. Let's say, for instance, that the window was resized. The dispatcher would post an event, passing the new size of the window as a parameter to the post function. The map "_events" stores all events posted in the current frame so that they will all be managed once before the beginning of the next frame. This technique is called "event polling." The basic idea is to collect all the events that have occurred and deal with them all at once. The other way around would be to directly manage events as they occur. One instance of why the second technique would not be the best solution for a game engine would be in a scenario where your engine is currently rendering your scene, and then suddenly, an event occurs right in the middle of the rendering process. Your engine would then have to stop the rendering process to first handle the event that occurred and then come back to finish the rendering of the scene. That can be a problem if an event occurs many times in a frame, as this will block the renderer from doing his job. On the other hand, the polling technique requires that we maintain the memory state to prevent memory overflow.

## Register Callback Functions

The second functionality is to register all callback functions for each event type. This is done using the add_callback() function. It takes a reference to a callback_function as parameter and stores it in the _callback map.

## Handle Events

The last job of the dispatcher is to dispatch all the events that occurred and call their callback functions. As you can see, both maps _events and _callback have the event_id of the event as the first data point of their pair, which makes it easy to find the callback function for each event type because each event has a unique typeid. The dispatch() function is the one in charge of calling all callback functions for each event type. We simply loop through the map of events that have occurred and find the callback function with the same event_id in the _callback map and execute it, passing the pointer to the event. We then finish the loop by calling the clear() function of the _events map to make sure the destructor of each event is called to free the memory.

## Example of Events

Go ahead and create a new folder called “events” with a header file called system.h. That folder will be used to create our custom event types.

```
engine/src/events/system.h
```

```
#pragma once
#include "core/event.h"

namespace fuse {
struct quit_event : event_instance {
    FUSE_INLINE quit_event() = default;
};
}
```

The code snippet above shows the definition of a custom event type that will be triggered when the window's close button is clicked.
Let us use this to test our event system. Update your inputs.h and inputs.cpp like shown in the code snippet below.

### engine/src/core/inputs.h

```
#pragma once
#include "dispatcher.h"

namespace fuse::inputs {
FUSE_API void initialize(SDL_Window*);
FUSE_API dispatcher* get_dispatcher();
FUSE_API void dispatch_events();
FUSE_API bool is_key(int);
}
```

### engine/src/core/inputs.cpp

```
#include "pch.h"
#include "inputs.h"
#include "events/system.h"

namespace fuse::inputs {
static const uint8_t* keyboard = NULL;
static dispatcher di_sp;

dispatcher* get_dispatcher() { return &di_sp; }

bool is_key(int key) { return keyboard[key]; }

void initialize(SDL_Window* window) {
    keyboard = SDL_GetKeyboardState(NULL);
}

void dispatch_events() {
    static SDL_Event event;
    while (SDL_PollEvent(&event)) {
        switch (event.type) {
        case SDL_QUIT: di_sp.post<quit_event>(); break;
        case SDL_KEYDOWN:
            keyboard = SDL_GetKeyboardState(NULL); break;
        case SDL_KEYUP:
            keyboard = SDL_GetKeyboardState(NULL); break;
        }
    }
    di_sp.dispatch();
}
}
```

As for the inputs.cpp file, we have a couple of new things going. First, we define a dispatcher object, then we implement the get_dispatcher() function, which simply returns the address of the dispatcher instance.

In the dispatch_events() function's while-loop, we have the SDL_QUIT event type, which is triggered when the user clicks on the window's close button. When that happens, we post a quit_event using our dispatcher.

Lastly, we call the dispatch() function of the dispatcher to handle all events that have occurred.

Now, go to your application.cpp and update your code like shown below.

### engine/src/core/application.cpp

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

We define a callback-function, on_quit() which simply changes the value of the is_running boolean to “false” when the window’s close button is clicked. This causes our game loop to stop its cycle. We use the dispatcher to register the function-callback. If we were in a class, we would register the function as below.

```
get_dispatcher()->add_callback<quit_event>(ORBIT_BIND(on_quit));
```

We would have needed our ORBIT_BIND macros to be able to register a member function of a class.

## More Events

Now that the foundation is established, we will use the same principle to add more events like mouse down, mouse up, and mouse scroll. The following code snippet shows a list of custom events.

### engine/src/events/system.h

```
#pragma once
#include "core/event.h"

namespace fuse {
struct quit_event : event_instance {
FUSE_INLINE quit_event() = default;
};

struct keydown_event : event_instance {
FUSE_INLINE keydown_event(int key) : key(key) {}
int key;
};

struct keyup_event : event_instance {
FUSE_INLINE keyup_event(int key) : key(key) {}
int key;
};

struct mousedown_event : event_instance {
FUSE_INLINE mousedown_event(int btn) : button(btn) {}
int button;
};

struct mouseup_event : event_instance {
FUSE_INLINE mouseup_event(int btn) : button(btn) {}
int button;
};

struct mousemotion_event : event_instance {
FUSE_INLINE mousemotion_event() = default;
};

struct mousewheel_event : event_instance {
FUSE_INLINE mousewheel_event() = default;
};
}
```

You can see the definition of mouse and key events added. If you wish, you can add more events like window maximized, minimized, etc. What we have here is enough to understand the principle. Let's also update the input system to manage all those new events.

### engine/src/core/inputs.cpp

```
#include "pch.h"
#include "inputs.h"
#include "events/system.h"

namespace fuse::inputs {
static const uint8_t* keyboard = NULL;
static dispatcher disp;

dispatcher* get_dispatcher() { return &disp; }
bool is_key(int key) { return keyboard[key]; }

void initialize(SDL_Window* window) {
    keyboard = SDL_GetKeyboardState(NULL);
}

void dispatch_events() {
    static SDL_Event event;
    while (SDL_PollEvent(&event)) {
        switch (event.type) {
        case SDL_QUIT: disp.post<quit_event>(); break;
        case SDL_MOUSEBUTTONDOWN:
            disp.post<mouse_down_event>(event.button.button); break;
        case SDL_MOUSEBUTTONUP:
            disp.post<mouse_up_event>(event.button.button); break;
        case SDL_MOUSEWHEEL: disp.post<mousewheel_event>(); break;
        case SDL_MOUSEMOTION:
            disp.post<mousemotion_event>(); break;
        case SDL_KEYDOWN:
            keyboard = SDL_GetKeyboardState(NULL);
            disp.post<keydown_event>(event.key.keysym.scancode);
        case SDL_KEYUP:
            disp.post<keyup_event>(event.key.keysym.scancode);
            keyboard = SDL_GetKeyboardState(NULL); break;
        }
        disp.dispatch();
    }
}
}
```

As you can see, we are now also able to post messages for mouse and key events. We are simply passing all SDL's event data to our post function to construct the event we want to post. All we have to do is just define and register callbacks functions for these events and we will be able to accomplish many things.
