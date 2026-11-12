```
// . . .

// create & start scene
auto scene = new ecs::scene(renderer);
scene->start();

scene->serialize("assets/scene.yaml");

last_tick = get_ticks();

while (is_running) {
    compute_delta_time();
    inputs::dispatch_events();
    SDL_RenderClear(renderer);
    scene->update(delta_time);
    SDL_RenderPresent(renderer);
}

// free memory
SDL_DestroyRenderer(renderer);
SDL_DestroyWindow(window);
FUSE_DELETE(scene);
IMG_Quit();
Mix_Quit();
TTF_Quit();
SDL_Quit();
}
}
```

All you have to do here to test the serializer is to call the serialize function, passing the target path, after the scene has started to make sure there are actually entities in the scene.

**Note :** The file stream will check if the filename you have passed exists and create it if not.

**Note :** The file extension can be anything of your choice. We are using the ".yaml" to make sure the output will be well formatted.

If you compile and run your project, you will get the YAML file below created in the following location **build/(Debug)/assets/scene.yaml**.