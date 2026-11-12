# "update_pipes" works.

engine/src/scripts/pipe_spawner.h

```
// . . .
FUSE_INLINE void update_pipes() {
    auto it = pipes.begin();
    while (it != pipes.end()) {
        // remove dead pipe
        auto& pipe = (*it);
        if (!pipe.is_alive()) {
            it = pipes.erase(it);
            continue;
        }
        it++;
    }
}
// . . .
```

The main job of the "update_pipes" function is to loop through the pipe list to check if any pipe is out of bounds and destroy it. This is really important because, without it, the memory size will increase every time a pair of pipes is created. A while loop is used because we want to be able to erase data from the array while looping through it.

Before we take a look at the “on_update” function, I want you to define the following function in your math folder because it will be used to generate random numbers.

engine/src/math/random.h

```
#pragma once
namespace fuse::math {
    FUSE_INLINE int random(int min, int max) {
        static bool first = true;
        if (first) {
            srand(time(NULL)); // seeding for the first time only!
            first = false;
        }
        return min + rand() % ((max + 1) - min);
    }
}
```