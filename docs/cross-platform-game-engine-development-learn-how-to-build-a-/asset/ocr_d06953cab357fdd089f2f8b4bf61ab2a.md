There are three key things you must do in this situation: Include your asset registry's header file, create a member variable called "_assets" in the asset registry, and modify your start() function as shown above. We're just adding an animation asset to the registry, as well as two texture assets that will be used as frames in the animation.

**Compile, run, and use the debugger** to check if everything is working as expected. You can also print out certain values to see if they match your expectations. We will see how to load textures-, fonts-, and audios assets from files in the upcoming chapters.

To give your ecs::system access to the asset registry we just created in the scene, update your system as indicated below. This will be important later when we start adding systems like the sprite renderer and the animator, etc.

```
engine/src/ecs/system.h
#pragma once
#include "entity.h"
#include "assets/registry.h"

namespace fuse::ecs {
struct system {
    FUSE_NO_INLINE virtual ~system() = default;

    FUSE_NO_INLINE void prepare(registry* rg, SDL_Renderer* rd, asset_registry* as) {
        this->rg = rg;
        this->renderer = rd;
        this->_assets = as;
    }

    template<typename T>
    FUSE_NO_INLINE auto view() {
        std::vector<entity> entities;
        for (auto& e : _registry->view<T>()) {
            entities.push_back(entity(e, _registry));
        }
        return entities;
    }

    FUSE_NO_INLINE virtual void update(float) {}
    FUSE_NO_INLINE virtual void start() {}

protected:
    SDL_Renderer* _renderer = NULL;
    asset_registry* _assets = NULL;
    registry* _registry = NULL;
};
};
```