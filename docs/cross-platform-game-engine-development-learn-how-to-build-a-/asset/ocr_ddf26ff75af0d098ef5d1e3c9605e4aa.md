# Sprite Component

If you remember from the ECS chapter, we said we would create our components in categories to reduce the number of inclusion statements because it has a beneficial effect on the compile time. The first category we created was found in ecs/components/common.h.

Let's now create another category in a new file called graphics.h. We will create all the components related to graphics in this file. Below is the code snippet of the sprite component.

```
engine/src/ecs/components/graphics.h
#pragma once
#include "assets/asset.h"
namespace fuse::ecs {
struct sprite_component {
    FUSE_INLINE sprite_component( const sprite_component& ) = default;
    FUSE_INLINE sprite_component() = default;
    SDL_RendererFlip flip = SDL_FLIP_NONE;
    asset_id sprite = INVALID_ID;
};
}
```

This component only has an asset_id and a flag called "flip," which defines the orientation of the sprite. SDL_RendererFlip is an enumeration of flags that can be used to set the orientation of a sprite while rendering it. Here are the possible values it could take:

| SDL_FLIP_NONE | do not flip |
| SDL_FLIP_HORIZONTAL | flip horizontally |
| SDL_FLIP_VERTICAL | flip vertically |

Only when required will the texture associated with the asset id be fetched and utilized. This method is useful for serialization. We can serialize components that have assets without knowing the contents of the asset itself. It also paves the way for multithreading. Because, for example, while loading a scene, we may delegate the loading of assets and components to multiple threads. This will improve our engine's capacity to load scenes and assets.

It is best practice to include a default constructor and a copy constructor in all your components because you want to be able to attach the component to an object without having to write any code.