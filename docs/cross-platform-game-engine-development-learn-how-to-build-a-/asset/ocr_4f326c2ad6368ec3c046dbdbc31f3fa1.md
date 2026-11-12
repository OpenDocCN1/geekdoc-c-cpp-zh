# TileMap Component

engine/src/ecs/components/graphics.h

```
struct tilemap_component {
    FUSE_INLINE tilemap_component(const tilemap_component&) = default;
    FUSE_INLINE tilemap_component() = default;
    asset_id tilemap = INVALID_ID;
};
```

The next component we will add to the **graphics.h** header file is the **tile map component**. This component, just as the **sprite_component** or even the **animation component**, simply stores the **asset_id** of a tile map asset. There isn't much we can say about this component.