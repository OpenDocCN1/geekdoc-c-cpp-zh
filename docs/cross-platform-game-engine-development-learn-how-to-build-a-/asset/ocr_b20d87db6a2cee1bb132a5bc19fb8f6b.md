```
// ...

// serialize animation_component
FUSE_INLINE void serialize_animation(YAML::Emitter& em, entity& e) {
    if (e.has_component<animation_component>()) {
        auto& a = e.get_component<animation_component>();
        em << YAML::Key << "animation_component";
        em << YAML::BeginMap;
        em << YAML::Key << "animation" << YAML::Value << a.animation;
        em << YAML::Key << "flip" << YAML::Value << (int)a.flip;
        em << YAML::EndMap;
    }
}
```

```
// deserialize animation_component
FUSE_INLINE void deserialize_animation(YAML::Node node, entity& e) {
    if (auto data = node["animation_component"]) {
        auto& a = e.add_component<animation_component>();
        a.flip = (SDL_RendererFlip)data["flip"].as<int>();
        a.animation = data["animation"].as<asset_id>();
    }
}
```

# Text Component Serialization