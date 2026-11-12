components of the entity.
To solve that problem, we will add a couple of implementations for the add-, get-, remove component functions here as protected member functions. So, add the following code snippet in your script instance struct.

# engine/src/scripts/script_instance.h

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