```
// serialize sprite_component
FUSE_INLINE void serialize_sprite(YAML::Emitter& em, entity& e) {
    if (e.has_component<sprite_component>()) {
        auto& s = e.get_component<sprite_component>();
        em << YAML::Key << "sprite_component";
        em << YAML::BeginMap;
        em << YAML::Key << "sprite" << YAML::Value << s.sprite;
        em << YAML::Key << "flip" << YAML::Value << s.flip;
        em << YAML::EndMap;
    }
}
```

```
// deserialize sprite_component
FUSE_INLINE void deserialize_sprite(YAML::Node node, entity& e) {
    if (auto data = node["sprite_component"]) {
        auto& s = e.add_component<sprite_component>();
        s.flip = (SDL_RendererFlip)data["flip"].as<int>();
        s.sprite = data["sprite"].as<asset_id>();
    }
}
```

# Animation Component Serialization