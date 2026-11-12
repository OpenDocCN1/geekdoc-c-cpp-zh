
## Script Component

We are going to create another category of components in a new header file called “behaviour.h”. Below is the code snippet of the script component’s definition.
engine/src/ecs/components/behaviour.h

```
#pragma once
#include "scripts/script_i_instance.h"

namespace fuse::ecs {
struct script_component {
FUSE_INLINE script_component(const script_component&) = default;
FUSE_INLINE script_component() = default;

template <typename T>
FUSE_INLINE void bind() {
instantiate = [](const script_props& props) {
auto script = static_cast<script_i_instance*>(new T());
script->init(props);
return script;
}};

script_i_instance* instance = NULL;
script_instantiator instantiate;
std::string name;
};
```

In the member variable section, we have a pointer to a script instance, an instantiator, and the name of the script. As you can see, the member function bind() is used to set the value of that lambda expression “instantiate” which will be called to create the script instance. Don’t worry, it will make sense in a moment.

## Script System

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
e.get_component<script_component>().instance->on_update(e, dt);
}
}
};
}
```

As you can see, we are calling the start function of each entity's script in the start function of the script system and the update function of the entity's script component in the update function of the script system.
We also want to make sure that the memory allocated for each script instance is also deallocated. That's why we have the destructor of the system defined.

## Collision Callback

If you look closely at the definition of the script instance, you will see that it also has a function called on_collision(ecs::entity). This function should be called when the entity with the script collides with another entity. The entity with whom he collided will be passed as an argument so that further actions can be taken against that entity. However, in the script system, we are unable to invoke that function. That's why we are going to update the code of the collision system so that the on_collision() function can be called when an entity with a script is colliding with another.

```
engine/src/ecs/systems/collision_system.h

FUSE_INLINE void update(float) {
    // get entity list
    auto entities = view<collider_component>();

    for (auto& e : entities) {
        auto& tr = e.get_component<transform_component>();
        auto& c1 = e.get_component<collider_component>();

        // update box collider offset
        c1.collider.x = tr.translate.x;
        c1.collider.y = tr.translate.y;

        // continue if disabled
        if(c1.disabled) { continue; }

        // check collision with others
        for (auto& o : entities) {
            if (o == e) { continue; }
            auto& c2 = o.get_component<collider_component>();
            if(check_collision(c1.collider, c2.collider)) {
                if(e.has_component<script_component>()) {
                    auto& script = e.get_component<script_component>();
                    script.instance->on_collision(o);
                }
            }
        }
    }
}
```

The code snippet above shows how the collision system's update function has been modified to call the script on_collision() function. The only thing we had to do here was to make sure that every time there is a collision, we check if the entity has a script component. If it does, we will call the on_collision() function, passing the entity it has collided with as an argument for further use.
There it is! We have a ready-to-use script system in place. We now want to test it by creating a player controller script that will allow us to move an object using the keys A, S, D, and W.

## Player Controller Script

This section is about creating a script that will allow us to move an entity using the keyboard. Go ahead and create a new header file in your scripts folder called player_controller.h.

The next code snippet is the definition of the player controller script.

```
engine/src/scripts/player_controller.h
#pragma once
#include "script_instance.h"
namespace fuse {
struct player_controller : script_instance {
FUSE_INLINE void on_start() {
FUSE_INFO("player_script started!");
}
FUSE_INLINE void on_collision(ecs::entity e) {
FUSE_INFO("colliding with: %d", e.id());
}
FUSE_INLINE void on_update(float dt) {
auto& t = get_component<ecs::transform_component>();
if(inputs::is_key(SDL_SCANCODE_A)) { // move left
t.translate.x -= (speed * dt);
}
if(inputs::is_key(SDL_SCANCODE_D)) { // move right
t.translate.x += (speed * dt);
}
if(inputs::is_key(SDL_SCANCODE_W)) { // move up
t.translate.y -= (speed * dt);
}
if(inputs::is_key(SDL_SCANCODE_S)) { // move down
t.translate.y += (speed * dt);
}
}
private:
float speed = 300.0f;
};
```

This script defines some functions from the parent script class. The update() function retrieves the transform component of the entity and updates its value according to the key pressed. SDL has a specific type to represent each key on the keyboard called **SDL_Scancode**. It is basically an enumeration of the SDL keyboard scan code representation. You can see the full list of key codes here [11].

You can simply use IntelliSense by just typing **SDL_SCANCODE_** to find any key's scan code.
Let's attach this script to an entity in the scene and see if our script system is working as expected.

## Testing the Player Controller Script

Register the script system in your scene's constructor and add some entities as shown in the next code snippet.

```
engine/src/ecs/scene.h
FUSE_INLINE void start() {
// load sprite
auto spl = _assets.load_texture("assets/obj 1.png", "", _renderer);
auto sp2 = _assets.load_texture("assets/obj 2.png", "", _renderer);

// add tilemap entity
auto e1 = add_entity("entity1");
e1.add_component<script_component>().bind<player_controller>();
e1.get_component<transform_component>().translate.x = 500;
e1.add_component<sprite_component>().sprite = spl->id;
e1.add_component<collider_component>();

auto e2 = add_entity("entity2");
e2.add_component<sprite_component>().sprite = sp2->id;
e2.add_component<collider_component>();

// start systems
for (auto& sys : _systems) { sys->start(); }
}
```

If you compile and run your project, you will be able to use the keys A, S, D, and W to move entity2 around, and if you hit the second entity, you will see some collision messages getting printed in the terminal.

## Fuse2D

![](img/2763810ed0a1572c2bec59ee52dd75be_185_0.png)

```
[info] player_script started!
[info] colliding with: 2
[info] colliding with: 2
```

## Conclusion

We are now officially ready to create a game with this engine. I really want to congratulate you on not giving up. I hope you are proud of yourself.

In the next chapter, we will create a simple shooter game to connect all the pieces we have so far.

If for some reason your code is not compiling or running properly, you can still clone the code from GitHub and learn from it. All the changes made so far are found in the branch "scripting".

## Chapter 13

### Making a Game

## Making a Game

![](img/2763810ed0a1572c2bec59ee52dd75be_188_0.png)

Building a game engine without thinking about how it could be used to make a game is dangerous. But you don’t have to worry because I did my homework. This chapter is going to be about making a simple shooter game using all the pieces we have added to this engine so far. The Figure 38 is a screenshot of the game we are going to build in this chapter. It is a replicate of the well-known game called “Flappy Bird”.

Flappy Bird is a 2013 Mobile App developed by Vietnamese developer Dong Nguyen and published by Gears Studios. The app was originally developed for Android and for the iPhone 5 in May 2013, later for iOS 6 and then in September 2013 for iOS 7. [23]

Figure 38 Flappy Plane

All we need to make this game is a background image, a sprite for the player or the plane, a sprite for the scrolling ground, a font file to display the score, and two sound effects, one for the background music and one for when the player dies. All assets used to make the
