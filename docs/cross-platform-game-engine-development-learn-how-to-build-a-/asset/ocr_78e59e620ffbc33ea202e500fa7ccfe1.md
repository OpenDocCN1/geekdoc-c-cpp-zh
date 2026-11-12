# # Tile Component

The tile component needs a little bit more data compared to the tile map component. First, a tile needs to know which tile map it belongs to, Secondly, it is important for that tile to also know from which tile set its texture is coming from; it also has to know which part of that tile set to render and, finally, where it will be rendered on the screen. Since the tile set is simply a grided texture, we can simply store the row and the column of the tile. The following image gives a visual idea of the concept.

![](bbox=[0.08, 0.24, 0.92, 0.43])

As you can see, the counting of rows and columns starts at zero and ends at n-1. Below is the code for the tile component. Add the code to your graphics.h header file right after the tile map component.
engine/src/ecs/components/graphics.h

```
struct tile_component {
    FUSE_INLINE tile_component( const tile_component& ) = default;
    FUSE_INLINE tile_component() = default;
    SDL_RendererFlip flip = SDL_FLIP_NONE;
    asset_id tilemap = INVALID_ID;
    asset_id tileset = INVALID_ID;
    float offset_x, offset_y = 0;
    int row col = 0;
};
```

We are going to render a tile set to test our system. Basically, we will break this texture into multiple tiles of size 64x64 and render each. Now that all components are ready, let's create the tile map system.