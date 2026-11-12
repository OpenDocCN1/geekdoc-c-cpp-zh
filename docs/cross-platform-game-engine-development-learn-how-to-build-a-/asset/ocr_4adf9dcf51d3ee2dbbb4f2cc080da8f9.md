```
// ...

// serialize text_component
FUSE_INLINE void d serialize_text(YAML::Emitter& em, entity& e) {
if (e.has_component<text_component>()) {
auto& t = e.get_component<text_component>();
em << YAML::Key << "text_component";
em << YAML::BeginMap;
em << YAML::Key << "R" << YAML::Value << (int)t.color.r;
em << YAML::Key << "G" << YAML::Value << (int)t.color.g;
em << YAML::Key << "B" << YAML::Value << (int)t.color.b;
em << YAML::Key << "A" << YAML::Value << (int)t.color.a;
em << YAML::Key << "text" << YAML::Value << t.text;
em << YAML::Key << "font" << YAML::Value << t.font;
em << YAML::Key << "flip" << YAML::Value << t.flip;
em << YAML::EndMap;
}
}

// deserialize text_component
FUSE_INLINE void d deserialize_text(YAML::Node node, entity& e) {
if (auto data = node["text_component"]) {
auto& t = e.add_component<text_component>();
t.flip = (SDL_RendererFlip)data["flip"].as<int>();
t.text = data["text"].as<std::string>();
t.font = data["font"].as<asset_id>();
t.color.r = data["R"].as<int>();
t.color.g = data["G"].as<int>();
t.color.b = data["B"].as<int>();
t.color.a = data["A"].as<int>();
}
}

// ...
```

# Script Component Serialization