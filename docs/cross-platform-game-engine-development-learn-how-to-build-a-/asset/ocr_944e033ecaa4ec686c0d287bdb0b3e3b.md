# Animation System

Below is the code for the animation system. The two lines highlighted are the only ones that need an explanation because the rest is the same as in the sprite renderer system.

We are using the function macro get_ticks_ms() to get the amount of time elapsed since the initialization of SDL in milliseconds. If you remember, in the chapter about Window and Events, we mentioned the fact that our animation and motion would not be frame-based but time-based instead. This is it; we use the current time to calculate which frame of the animation must be rendered to the screen. The modulo “%” in the formula is to make sure we never get a frame index above the frame count of the current animation.

If you look at the definition of the animation, you will notice that it has an array of asset_ids. The frame index calculated is used to retrieve the asset_id of the frame we want to render from that array. The retrieved asset_id is then used to get the texture asset from the asset registry.

We are going to use the following frames to test the animation system. Feel free to use any free asset you find online. Sorry am not a graphic artist*.

![](bbox=[0.081, 0.447, 0.714, 0.562])

engine/src/ecs/systems/frame_animation_system.h