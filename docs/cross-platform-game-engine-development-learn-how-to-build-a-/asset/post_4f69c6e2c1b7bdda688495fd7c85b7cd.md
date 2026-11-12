
collision system to initialize the position of all colliders.
For debugging purposes, we want to render the shape of the box colliders. To do
that, we simply use the SDL built-in function to render SDL_FRect.

If you compile and run your code, you will see two objects moving in opposite
directions with their box collider, as shown in the picture below.

![](img/2763810ed0a1572c2bec59ee52dd75be_171_0.png)

the following message will be printed in the terminal when they collide.

```
[info] collision: 2 -> 1
[info] collision: 1 -> 2
[info] collision: 2 -> 1
[info] collision: 1 -> 2
```

You can play around with the collision system by doing something else when the
collision happens than just printing a message in the console. You could set the
gravity scale to a value different than zero so that the entities can fall when the
collision in detected.

```
if (check_collision(c1.collider, c2.collider)) {
    auto& rb = e.get_component<rigidbody_component>();
    rb.body.gravity_scale = 0.5f;
}
```

## Conclusion

This physics engine is insufficient for a game engine. There are numerous other simulations not covered in this book. But for the time being, what it has to offer is sufficient to make a good game.

Using a library like Box2D is a clever idea because it is well-known in the 2D game industry and has a lot more to offer in terms of 2D physics simulation.

Note: Feel free to clone the source code from the repository if you are facing any issues with your own code. You will find the current code’s version under the branch called “physics”.

## Chapter 12 Native Scripting

## Native Scripting

So far in this book, we have been adding features like texture, text rendering, animations, and physics simulations but we still don’t really know how to use it all to make a game. We do not want to forget that the main purpose of a game engine is to make games not just a bunch of features brought together.

That’s where scripting comes in. It will make it possible for us to use all the features we have added so far to create a game.

A scripting language, also known as a scripting language, is a programming language for a runtime system that automates the execution of processes that would otherwise be performed independently by a human operator.

Scripting languages are frequently interpreted rather than compiled. [26]

## Compiled and Interpreted Script

As you can see from the title, we are going to create a native scripting system. That means it is going to be the same programming language as the engine and it is also going to be a compiled not interpreted scripting system. This means that the script is written as part of the engine source code and is also compiled with the engine. An interpreted script compared to a compiled one is a little less efficient, but it offers the ability to be hot reloaded at runtime without the need of restarting the application but creating one like that requires knowledge of multiple programming languages and memory layout which is some we are not trying to do in this book. The compiled version has the advantage of being native which means better performance and a low level of complexity.

The following diagram shows an example of an interpreted scripting system using C# as a coding language. C# is one of the most widely used scripting languages because it is easy to integrate with C++ and because it is easy to understand.

![](img/2763810ed0a1572c2bec59ee52dd75be_175_0.png)

Figure 37 Example of a C#-Scripting Architecture

Unity3D and many other game engines use C# for scripting. There are also other languages like Lua, Java, JavaScript, etc. The C#-code in the diagram above will be compiled into a dynamic shared library that can be linked to the engine at runtime and the engine will simply call functions from the script to execute the developer's tasks.

Although this diagram appears to be simple, putting it together requires more effort than you may think. Maybe this will be a good topic for another book but for now, let's stick with the native scripting.

## Abstract Script

Since we will be having many scripts running through a single system, we have to somehow create a sort of pattern for all scripts. We want all scripts to have certain functions that we would be able to call without checking whether that function exists or not. That’s why we are going to use virtual functions and inheritance. This section is about creating a core class from which all scripts will inherit and decide whether they want to implement their own version of the virtual functions. Since this scripting system is quite tied to the entity component system, we want to make it easy to access the components of an entity in the registry. That’s why we are going to create a custom entity object which has access to the registry. That entity object will be used in our scripts to play around with entities. Let’s create the entity object first and the rest will be much clear.

### Creating The Script Instance

The next code snippet shows the definition of the script instance. Make sure to update your engine’s folder tree by creating the same file in the. As you can see, it is an abstract class with a bunch of virtual functions. In the member variables section, we have defined an entity id, a pointer to the asset registry and a pointer to the ecs::registry. The entity id is the game object with the script. The pointer to the asset registry is important because we want to have access to all assets in the script as well.

Right on top is a structure called script_props which is just a simple container we have defined to hold the parameters needed to initialize the script instance. We have a bunch of virtual functions that can be implemented in the derived scripts to perform custom behaviours on entities. The init() function is used to set the member variables to their proper values.

We also have the script_instantiator at the bottom which is a lambda function type that will be used to instantiate the script instance. C++ allows us to create inline functions with lambda expressions, which are useful for brief pieces of code that won’t be reused and aren’t worth naming. The script_instantiator function returns a pointer to a script instance and it takes script_props as an argument. That argument will be passed to the init() function of the script to set its member variables.

```
engine/src/scripts/script_instance.h
```

```
#pragma once
#include "ecs/components/graphics.h"
#include "ecs/components/physics.h"
#include "ecs/components/common.h"
#include "ecs/entity.h"

#include "assets/registry.h"
#include "core/inputs.h"

namespace fuse {
struct script_props {
FUSE_INLINE script_props(ecs::entity_id e, ecs::registry* r,
asset_registry* a):
entity(e), registry(r), assets(a) {}
ecs::entity_id entity = INVALID_ID;
ecs::registry* registry = NULL;
asset_registry* assets = NULL;
};

struct script_instance {
FUSE_INLINE virtual ~script_instance() = default;

FUSE_INLINE void init(const script_props& props) {
this->registry = props.registry;
this->assets = props.assets;
this->entity = props.entity;
}

FUSE_INLINE virtual void on_collision(ecs::entity) {}
FUSE_INLINE virtual void on_update(float) {}
FUSE_INLINE virtual void on_destroy() {}
FUSE_INLINE virtual void on_start() {}

private:
ecs::entity_id _entity = INVALID_ID;
ecs::registry* _registry = NULL;
asset_registry* _assets = NULL;
};

// script allocator function type
using script_instantiator = std::function<script_instance*(const script_props&)>;
}
```

Since the registry is a private member variable, it can't be accessed by any script that inherits from the script_instance. That means we won't be able to access the components of the entity.
To solve that problem, we will add a couple of implementations for the add-, get-, remove component functions here as protected member functions. So, add the following code snippet in your script instance struct.

### engine/src/scripts/script_instance.h

```
// ...
protected:
    template <typename T, typename... Args>
    FUSE_INLINE T& add_component(Args&&... args) {
        return _registry->add_component<T>(_entity, std::forward<Args>(args)...);
    }

    template <typename T>
    FUSE_INLINE T& get_component() {
        return _registry->get_component<T>(_entity);
    }

    template <typename T>
    FUSE_INLINE void remove_component() {
        return _registry->remove_component<T>(_entity);
    }

    template <typename T>
    FUSE_INLINE bool has_component() {
        return _registry->has_component<T>(_entity);
    }

    FUSE_INLINE ecs::entity add_entity() {
        auto entity = _registry->add_entity();
        _registry->add_component<ecs::transform_component>(entity);
        _registry->add_component<ecs::info_component>(entity);
        return ecs::entity(entity, _registry);
    }
// ...
```

We will now be able to easily access all valuable information about the entity that currently holds the script. The add_entity() function will add a new entity with some core component and return an entity object.

We now have everything we need to create a script component along with its system. The process remains the same, we create the component then the system and we test if everything works well together.
