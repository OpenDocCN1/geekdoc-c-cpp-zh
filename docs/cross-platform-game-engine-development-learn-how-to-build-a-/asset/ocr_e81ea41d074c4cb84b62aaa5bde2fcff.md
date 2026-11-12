are too many active scripts.
We have a Boolean called “game_over” which tells us if the plane has crashed or not. We will use the “time” to know when to spawn new pipes and finally we have the “score”.

```
engine/src/scripts/pipe_spawner.h
// ...
FUSE_INLINE void spawn_pipe(float x, float y) {
    auto pipe = add_entity();
    auto& tr = pipe.get_component<ecs::transform_component>();
    tr.translate = vec2f(x, y);

    // add rigid body
    auto& rb = pipe.add_component<ecs::rigidbody_component>();
    rb.body.gravity_scale = 0.0f;
    rb.body.velocity.x = -100.0f;

    // add sprite
    auto pipe_sprite = get_asset<texture_asset>("pipe pe");
    auto& sp = pipe.add_component<ecs::sprite_component>();
    sp.flip = (y < 0) ? SDL_FLIP_NONE : SDL_FLIP_VERTICAL;
    sp.sprite = pipe_sprite->id;

    // add collider
    auto& cl = pipe.add_component<ecs::collider_component>();
    cl.collider = {
        tr.translate.x,
        tr.translate.y,
        (float)pipe_sprite->instance.width,
        (float)pipe_sprite->instance.height
    };
    pipes.push_back(pipe);
}
// ...
```

Above is the pipe spawner script member function which is used to generate a pipe. It takes the position that the pipe must be generated as an argument.
As you can see we are creating an entity with a rigid body, sprite, and collider component. Because we always have to create a pipe from top to bottom and another one from bottom to top, we are checking if the position on the y-axis is smaller than zero to know if the sprite must be flipped vertically or not.
The size of the box collider is the same as the sprite size.
That is all we need to do to create a pipe. Let’s see how the function