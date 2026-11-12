```
```cpp
// . . .
FUSE_INLINE void on_update(float dt) {
if(game_over) { return; }
// find player
auto player = find_entity("player");
auto& p_rb = player.get_component<ecs::rigidbody_component>();
// check if player's rigidbody is disabled
if(player.is_alive() && p_rb.disabled) {
// stop ground scroll animation
auto ground = find_entity("ground");
auto& gd = ground.get_component<ecs::rigidbody_component>();
gd.disabled = true;
}
// show game over text
auto scr = find_entity("score");
auto& tx = scr.get_component<ecs::text_component>();
tx.text = "GAME OVER";
// stop all pipes motion
for(auto& pipe : pipes) {
auto& rb = pipe.get_component<ecs::rigidbody_component>();
rb.disabled = true;
auto& co = pipe.get_component<ecs::collider_component>();
co.disabled = true;
}
game_over = true;
return;
}
// update pipes
update_pipes();
// create pipes
if(time > 2.5f) {
time = 0.0f;
float space = math::random(60, 150);
spawn_pipe(380, -space);
spawn_pipe(380, 720/2 + space);
}
// update counter
time += dt;
}
// . . .
```
```

To show “Game Over” when the player dies, we are also changing the value of the score in the “on_update” function. As shown in the code snippet above. That