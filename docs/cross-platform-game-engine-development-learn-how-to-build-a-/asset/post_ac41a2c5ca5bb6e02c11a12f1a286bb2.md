
## Getting Mouse Data

What if we also want to get our mouse data just as we did for the keyboard? Let's say, for instance, you want to know the current position of your mouse, not based on the event but its current state. That's exactly what we are going to do.

- Custom Vector 2D

To make it easy for us to store our mouse data and perform two-dimensional operations easily, we need to have a custom vector2 type. The following picture describes how the coordinate system of SDL works.

![](img/2763810ed0a1572c2bec59ee52dd75be_80_0.png)

The top left corner of the screen is the origin of the coordinate system. Each object's position is also specified by its top-left corner, not its center. The position is represented by a two-dimensional vector with (x, y) values. Moving down will increase the y-value of the position and moving up will decrease it. Moving to the right will increase the x-value and moving up to the left will decrease it. Let's create our custom vector type.

Create a new folder in your project folder tree: engine/src/math and create a file called vec2.h with the following code.

```
engine/src/math/vec2.h
```

```cpp
#pragma once

namespace fuse::math {
template <typename T>
struct vec2 {
    T x = 0, y = 0;

    FUSE_INLINE vec2(T x, T y) : x(x), y(y) {}
    FUSE_INLINE vec2(T v) : x(v), y(v) {}
    FUSE_INLINE vec2() = default;

    // operator (+)
    FUSE_INLINE vec2<T> operator +(const vec2<T> &v2) const {
        return vec2<T>(this->x + v2.x, this->y + v2.y);
    }

    // operator (+=)
    FUSE_INLINE vec2<T> &operator +=(const vec2<T> &v2) {
        this->x += v2.x;
        this->y += v2.y;
        return *this;
    }

    // operator (-)
    FUSE_INLINE vec2<T> operator -(const vec2<T> &v2) const {
        return vec2<T>(x - v2.x, y - v2.y);
    }

    // operator (-=)
    FUSE_INLINE vec2<T> &operator -=(const vec2<T> &v2) {
        this->x -= v2.x;
        this->y -= v2.y;
        return *this;
    }

    // operator (*)
    FUSE_INLINE vec2<T> operator *(T s) const {
        return vec2<T>(x * s, y * s);
    }

    // operator (*=)
    FUSE_INLINE vec2<T> &operator *=(T scalar) {
        this->x *= scalar;
        this->y *= scalar;
        return *this;
    }
};
}
```

Again, we make use of the C++ template features to make our lives easier. The vec2 is a template struct, which implies it will be instantiated with a specified template type. Our vec2 type will not support any C++ math operator by default, so we must overload them ourselves. If you want to create a vec2 out of integers or floats, you'd define it like this:

```cpp
auto a = vec2<float>(1.0f);
auto b = vec2<int>(2, 4);
```

To reduce the number of codes we would write to define a vec2, we are going to define some typedefs with some commonly used template types.

```cpp
// . . .
engine/src/math/vec2.h
namespace fuse {
    using vec2u = vec2<uint32_t>;
    using vec2f = vec2<float>;
    using vec2i = vec2<int>;
}
```

We can define a vec2 like this:

```cpp
vec2f a(1.0f);
vec2i b(2, 4);
```

- Mouse Input

Now that we have our vec2 in place, let's create a container for the mouse's state. Update your input.h header file like shown below

engine/src/core/inputs.h

```cpp
#pragma once
#include "math/vec2.h"
#include "dispatcher.h"

namespace fuse::inputs {
struct mouse_state {
    std::bitset<7> buttons = {0};
    vec2f offset, wheel;
};

FUSE_API const vec2f& mouse_offset();
FUSE_API const vec2f& mouse_wheel();
FUSE_API bool is_button(int);

FUSE_API void initialize(SDL_Window*);
FUSE_API dispatcher* get_dispatcher();
FUSE_API void dispatch_events();
FUSE_API bool is_key(int);
}
```

The function **mouse_wheel()** returns the scrolled step for the horizontal and the vertical wheel, **mouse_offset()** returns the current position of the mouse and **is_button()** checks if a mouse button is currently down.

- engine/src/core/inputs.cpp

```cpp
#include "pch.h"
#include "inputs.h"
#include "events/system.h"

namespace fuse::inputs {
static const uint8_t* keyboard = NULL;
static mouse_state mouse;
static dispatcher dispatcher;

dispatcher* get_dispatcher() { return &dispatcher; }
bool is_key(int key) { return keyboard[key]; }
const vec2f& mouse_wheel() { return mouse.wheel; }
const vec2f& mouse_offset() { return mouse.offset; }
bool is_button(int b) { return mouse.buttons.test(b); }
```

```cpp
void initialize(SDL_Window* window) {
    keyboard = SDL_GetKeyboardState(NULL);
}
```

```cpp
void dispatch_events() {
    static SDL_Event event;
    while (SDL_PollEvent(&event)) {
        switch (event.type) {
        case SDL_QUIT: dispatcher.post<quit_event>(); break;
        case SDL_MOUSEBUTTONDOWN:
            mouse.buttons.set(event.button.button);
            dispatcher.post<mousedown_event>(event.button.button); break;
        case SDL_MOUSEBUTTONUP:
            mouse.buttons.reset(event.button.button);
            dispatcher.post<mouseup_event>(event.button.button); break;
        case SDL_MOUSEWHEEL:
            mouse.wheel = vec2f(event.button.x, event.button.y);
            dispatcher.post<mousewheel_event>(); break;
        case SDL_MOUSEMOTION:
            mouse.offset = vec2f(event.button.x, event.button.y);
            dispatcher.post<mousemotion_event>(); break;
        case SDL_KEYDOWN:
            keyboard = SDL_GetKeyboardState(NULL);
            dispatcher.post<keydown_event>(event.key.keysym.scancode);
        case SDL_KEYUP:
            dispatcher.post<keyup_event>(event.key.keysym.scancode);
            keyboard = SDL_GetKeyboardState(NULL); break;
        }
        dispatcher.dispatch();
    }
}
```

The structure **mouse_state** stores all the information about the mouse, like current position, wheel data, and button states. Feel free to add your custom data if you want. Every time a mouse event occurs, we make sure we update the state of the mouse accordingly. The lines highlighted are just to show which part of the code has changed.

- **Print mouse Position**

You can use the logger to print the current position of the mouse in the console when the left key is pressed as shown below.

```cpp
while (is_running) {
    if (inputs::is_button(SDL_BUTTON_LEFT)) {
        auto mouse = inputs::mouse_offset();
        FUSE_INFO("%f, %f", mouse.x, mouse.y);
    }
}
```

```
[info] (725.000000, 15.000000)
[info] (725.000000, 15.000000)
[info] (725.000000, 15.000000)
[info] (725.000000, 15.000000)
```

## Conclusion

I am glad you made it so far! If for some reason your code did not make it, don't worry because I got your back. There is a specific branch on the GitHub repository ready to be cloned and used. The name of the branch is **window-inputs**. The link to the repository is still the same.

> **Note :** Remember to always make the **build-linux.sh** file executable on Linux if you clone the repository.

In the upcoming chapter, we will build our entity-component system which is a central piece of our engine.

## Chapter 5

### Entity Component System

ECS, or Entity Component System, is a design that separates data from behaviour to promote code reuse. Data is usually cache-friendly saved, which enhances performance and memory usage.

The cache memory is a chip-based computer component that improves the efficiency with which data is retrieved from the computer's storage. It serves as a temporary storage area from which the computer's processor may easily retrieve data. This temporary storage area, known as a cache, is available to the processor more easily and quickly than the computer's main work storage (DRAM).

An ECS has the following characteristics:

- It has entities, which are identifiers that are unique.
- components are just datatypes with no behaviour.
- Entities might have a single component or several components.
- Entities can change components on the fly.
- Behaviours are implemented in systems that target entities with a certain set of components.

### Alternatives to ECS

To understand why the ECS is a smart choice for building our game engine, we must first look at the alternatives. We are going to look at the object-oriented design, component-oriented design, and data-oriented design. Our comparison will be done using the following categories:

- Performance and Maintenance
- CPU Cache and Memory Usage

#### Object-Oriented Design

On the surface, it appears that object-oriented (OO) programming is an excellent choice for creating games because games are simply a collection of objects interacting in a scene. This design, however, has numerous flaws that have caused many game developers to abandon it.

![](img/2763810ed0a1572c2bec59ee52dd75be_88_0.png)

A typical OO design for a game will look like the picture above. At the top, we have an interface Object that contains pure virtual functions like update(), destroy(), render() that must be implemented by all child classes like GameObject and UIObject. The picture above shows three levels of inheritance which means we also have three levels of virtual lookup-table. This can have a massive impact on performance as the processor will have to look up the table to find the proper function to call.

In the image above, we have a child class called Player as well as another one called Boss. What if we want a Boss who is also a Player? This is where things get strange with the OO design because we'll have to use multiple inheritance, which is already a bad idea as it would make it even more difficult to maintain.

Since all objects must inherit from the "Object" interface, we must allocate
