![](bbox=[0.08, 0.06, 0.46, 0.16])

for the player. The first sprite in the left is used when the plane is flying and the second when it has crashed.

Let's return to the scene and add a player entity. Below is the code snippet.

```
FUSE_INLINE void start() {
 // ...
 // // player
 auto & player = add_entity("player");
 auto & ps = player.add_component<ecs::script_component>();
 ps.bind<player_controller>();
 ps.name = "player_controller ";
 auto & tr = player.add_component<transform_component>();
 tr.translate = vec2f({126, 360});
 tr.scale = vec2f(0.5f);
 auto & rb = player.add_component<rigidbody_component>();
 rb.body.gravity_scale = 25.0f;
 player.add_component<sprite_component>().sprite = fly_id;
 auto & cl = player.add_component<collider_component>();
 cl.collider = { 0, 0, 58, 38 };
 // start systems
 for (auto & sys : _systems) { sys->start(); }
}
```

We are adding an entity with a script component. We haven't so far used the name of the script component for any purpose, but it is important to set its value because we will use it later to serialize and deserialize the scene. Serialization will be implemented in the next chapter.

The player also has a rigid body and a collider component. The size of the box collider fits the sprite I am using. So, make sure to set your own values if you are using a different sprite for the plane. We are getting the transform component of the player to set its initial position, which is basically the center of the screen. We have to increase the value of the gravity scale to also increase the effect of gravity on the plane.

If you compile and run your code, you will be able to use the space key to keep the plane I the air. But if you hit the ground, the player sprite will change, and it