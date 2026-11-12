```
protected:
// ...
FUSE_INLINE void destroy() {
    _registry->destroy(_entity);
}

FUSE_INLINE ecs::entity find_entity(const std::string& name) {
    for(auto& e : _registry->view<ecs::info_component>()) {
        auto& i = _registry->get_component<ecs::info_component>(e);
        if(!i.name.compare(name)) {
            return ecs::entity(e, _registry);
        }
    }
    return ecs::entity();
}

template <typename T>
FUSE_INLINE T* get_asset(const std::string& name) {
    return _assets->get<T>(name);
}
// ...
```

The first function “destroy” can be used to delete the entity that is currently holding the script. The second “find_entity” function looks for an entity using the name provided as an argument. Finally, we have a method that takes a string, a template type and returns an asset pointer. This function will search the asset of type “T” with the name supplied as augment.

# Adding Background Sprite

The background of the game’s scene is nothing but just an entity with a sprite component attach to it. Next is a code snippet that shows how the background entity is added to scene.

+   engine/src/ecs/scene.h