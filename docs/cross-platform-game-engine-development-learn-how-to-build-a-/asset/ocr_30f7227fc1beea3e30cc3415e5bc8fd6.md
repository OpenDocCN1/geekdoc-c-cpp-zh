# Script System

The primary job of the script system is to target all entities with a script component, instantiate their script instances, and call their **on_start()** and **on_update()** functions. Below is the code snippet of the script system.

```
#pragma once
#include "ecs/system.h"

namespace fuse::ecs {
struct script_system {
FUSE_INLINE ~script_system() {
for (auto& e : view<script_component>()) {
auto& script = e.get_component<script_component>();
FUSE_DELETE(script.instance);
}
}

FUSE_INLINE void start() {
for (auto& e : view<script_component>()) {
auto& script = e.get_component<script_component>();
script.props(e, _registry, _assets);
script.instance = script.instantiate(props);
script.instance->on_start();
}
}

FUSE_INLINE void update(float dt) {
for (auto& e : view<script_component>()) {
e.get_component<script_component>().instance->on_up-
date(e dt);
}
}
};
}
```

As you can see, we are calling the start function of each entity's script in the start function of the script system and the update function of the entity's script component in the update function of the script system.
We also want to make sure that the memory allocated for each script instance is also deallocated. That's why we have the destructor of the system defined.

# Collision Call back

If you look closely at the definition of the script instance, you will see that it also