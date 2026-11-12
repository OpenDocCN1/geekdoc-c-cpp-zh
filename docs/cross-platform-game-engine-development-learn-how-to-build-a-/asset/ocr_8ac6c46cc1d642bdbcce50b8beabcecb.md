The asset serializer is similar to the entity serializer. We have two main functions to de- and serialize all asset types using each asset type custom de- and serialize function.

The deserilize function takes the renderer as parameter because it is required to load textures in SDL.

We will also add other functions to de- and serialize other asset types later.

To make it possible for the asset serializer to access the map inside of the asset registry, we are going to make the asset serializer class a friend of the asset registry class.

The next code snippet shows how it is done.

```
engine/src/assets/registry.h
#pragma once
#include "font.h"
#include "audi o.h"
#include "till emap.h"
#include "texture .h"
#include "animation .h"
#include "core/ typei d.h"
namespace fuse {
struct asset_registry {
    FUSE_NONIE asset_registry() = default;
    // . . .
private:
    friend struct asset_serializer;
    std::unordered_map<asset_typeid, std::vector<asset*>> _data;
};
}
```

The friend declaration appears in a class body and grants a function or another class access to private and protected members of the class where the friend declaration appears. [3]

This will make it possible for the asset sterilizor to access the "_data" member variable. We could have implemented a function that returns a reference to the data map.

# Implementation of Member Functions

The next code snippet shows the implementation of the main de- and serializes functions of the asset serializer.