

资产序列化器与实体序列化器类似。我们有两个主要函数，使用每种资产类型自定义的反序列化和序列化函数来对所有资产类型进行反序列化和序列化。

反序列化函数将渲染器作为参数，因为在 SDL 中加载纹理需要它。

我们稍后还会添加其他函数来对其他资产类型进行反序列化和序列化。

为了使资产序列化器能够访问资产注册表内部的映射，我们将把资产序列化器类设为资产注册表类的友元。

下一个代码片段展示了具体做法。

```
engine/src/assets/registry.h
#pragma once
#include "font.h"
#include "audio.h"
#include "tilemap.h"
#include "texture.h"
#include "animation.h"
#include "core/typeid.h"
namespace fuse {
struct asset_registry {
    FUSE_NOEXCEPT asset_registry() = default;
    // . . .
private:
    friend struct asset_serializer;
    std::unordered_map<asset_typeid, std::vector<asset*>> _data;
};
}
```

友元声明出现在类体中，并授予函数或另一个类访问友元声明所在类的私有和受保护成员的权限。[3]

这将使资产序列化器能够访问 "_data" 成员变量。我们本可以实现一个返回数据映射引用的函数。

## 成员函数的实现

下一个代码片段展示了资产序列化器的主要反序列化和序列化函数的实现。

```
engine/src/assets/serializer.h
// . . .

// serialize all asset types
FUSE_INLINE void serialize(YAML::Emitter& em) {
    em << YAML::Key << "assets" << YAML::Value << YAML::BeginSeq;
    {
        // serialize animations
        serialize_animations(em);

        // serialize textures
        serialize_textures(em);

        // serialize audios
        serialize_audios(em);

        // serialize fonts
        serialize_fonts(em);
    }
    em << YAML::EndSeq;
}

// deserialize all asset types
FUSE_INLINE void deserialize(YAML::Node& nodes, SDL_Renderer* r) {
    // clear registry
    _assets->clear();

    // deserialize assets
    for (auto node : nodes) {
        deserialize_texture(node, r);
        deserialize_animation(node);
        deserialize_audio(node);
        deserialize_font(node);
    }
}

// . . .
```

与实体序列化器类似，我们只需为每种资产类型调用一个自定义函数来序列化资产。序列化函数的唯一区别在于，我们将在一个函数中序列化特定类型的所有资产。

让我们实现所有用于反序列化和序列化所有资产类型的函数。以下函数均在资产序列化器中实现。“engine/src/assets/serializer.h”

## 纹理资产序列化

```
// ...
// serialize texture_asset
FUSE_INLINE void serialize_textures(YAML::Emitter& em) {
    for (auto asset : _assets->data | type_id<texture_asset>) {
        auto texture = static_cast<texture_asset*>(asset);
        em << YAML::BeginMap;
        {
            em << YAML::Key << "texture";
            em << YAML::BeginMap;
            {
                em << YAML::Key << "id" << YAML::Value << texture->id;
                em << YAML::Key << "name" << YAML::Value << texture->name;
                em << YAML::Key << "source" << YAML::Value << texture->instance.filename;
            }
            em << YAML::EndMap;
        }
        em << YAML::EndMap;
    }
}
// deserialize texture_asset
FUSE_INLINE void deserialize_texture(YAML::Node node, SDL_Renderer* target) {
    if (auto data = node["texture"]) {
        auto source = data["source"].as<std::string>();
        auto name = data["name"].as<std::string>();
        auto asset = _assets->load_texture(source, name, target);
        asset->id = data["id"].as<asset_id>();
    }
}
// ...
```

## 动画资产序列化

```cpp
// . . .

// serialize animation_asset
FUSE_INLINE void serialize_animations(YAML::Emitter& em) {
    for (auto asset : _assets->data | type_id<animation_asset>) {
        auto anim = static_cast<animation_asset*>(asset);
        em << YAML::BeginMap;
        {
            em << YAML::Key << "animation";
            em << YAML::BeginMap;
            {
                em << YAML::Key << "id" << YAML::Value << anim->id;
                em << YAML::Key << "name" << YAML::Value << anim->name;
                em << YAML::Key << "speed" << YAML::Value << anim->instance.speed;
            }
            // serialize frames
            for (int i = 0; i < anim->instance.frames.size(); i++) {
                auto temp = "frame" + std::to_string(i);
                em << YAML::Key << temp << YAML::Value << anim->instance.frames[i];
            }
            em << YAML::EndMap;
        }
        em << YAML::EndMap;
    }
}

// deserialize animation_asset
FUSE_INLINE void deserialize_animation(YAML::Node node) {
    if (const auto data = node["animation"]) {
        auto name = data["name"].as<std::string>();
        auto asset = _assets->add<animation_asset>(name);
        // deserialize frames
        int i = 0;
        while (true) {
            auto temp = "frame" + std::to_string(i);
            if (!data[temp]) { break; }
            auto frame = data[temp].as<asset_id>();
            asset->instance.frames.push_back(frame);
            i++;
        }
    }
    asset->instance.speed = data["speed"].as<int>();
    asset->id = data["id"].as<asset_id>();
}
```

由于动画的帧数是相对的，在处理动画帧时需要使用循环。每个帧都使用键 "frame" 加上其索引进行序列化存储。"frame0, frame1, frame2"。

## 音频资产序列化

```
// ...

// serialize audio_asset
FUSE_INLINE void serialize_audio(YAML::Emitter& em) {
    for (auto asset : _assets->data[type_id<audio_asset>()]) {
        auto audio = static_cast<audio_asset*>(asset);
        em << YAML::BeginMap;
        {
            em << YAML::Key << "audio";
            em << YAML::BeginMap;
            {
                em << YAML::Key << "id" << YAML::Value << audio->id;
                em << YAML::Key << "name" << YAML::Value << audio->name;
                em << YAML::Key << "source" << YAML::Value << audio->instance.filename;
            }
            em << YAML::EndMap;
        }
        em << YAML::EndMap;
    }
}

// deserialize audio_asset
FUSE_INLINE void deserialize_audio(YAML::Node node) {
    if (auto data = node["audio"]) {
        auto name = data["name"].as<std::string>();
        auto source = data["source"].as<std::string>();
        auto asset = _assets->load_audio(source, name);
        asset->id = data["id"].as<asset_id>();
    }
}

// ...
```

## 字体资产序列化

```cpp
// . . .

// serialize font_asset
FUSE_INLINE void serialize_fonts(YAML::Emitter& em) {
    for (auto asset : _assets->data | type_id<font_asset>) {
        auto font = static_cast<font_asset*>(asset);

        em << YAML::BeginMap;
        {
            em << YAML::Key << "font";
            em << YAML::BeginMap;
            {
                em << YAML::Key << "id" << YAML::Value << font->id;
                em << YAML::Key << "name" << YAML::Value << font->name;
                em << YAML::Key << "size" << YAML::Value << font->instance.size;
                em << YAML::Key << "source" << YAML::Value << font->instance.filename;
            }
            em << YAML::EndMap;
        }
        em << YAML::EndMap;
    }
}

// deserialize font_asset
FUSE_INLINE void deserialize_font(YAML::Node node) {
    if (auto data = node["font"]) {
        auto size = data["size"].as<float>();
        auto name = data["name"].as<std::string>();
        auto source = data["source"].as<std::string>();
        auto asset = _assets->load_font(source, name, size);
        asset->id = data["id"].as<asset_id>();
    }
}
```

