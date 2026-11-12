

```cpp
#pragma once
#include "asset.h"

namespace fuse {
struct animation {
std::vector<asset_id> frames;
int speed = 100;
};

struct animation_asset : asset {
FUSE_INLINE animation_asset() = default;
animation instance;
};
}
```

## 瓦片地图资源

瓦片地图在 2D 游戏中非常常见。它们通过使用称为瓦片的规则形状图像来构建游戏世界。超级马里奥、吃豆人甚至塞尔达传说等一些流行游戏都使用这种技术来构建关卡。瓦片地图除了可以带来性能改进外，还可以映射到逻辑网格，并且可以在游戏逻辑中以多种方式使用（例如，处理碰撞、实现 AI），或用于构建关卡编辑器。[20]

![](img/2763810ed0a1572c2bec59ee52dd75be_113_0.png)

图 27 瓦片地图

存储一组瓦片最有效、最常用的方式是通过瓦片集。它本质上就是将你需要的所有瓦片放在一个轻量级图像文件中。到了需要在屏幕上绘制瓦片的时候，只会使用较大图像中的一小部分。下面是用于创建上述场景的瓦片集。

![](img/2763810ed0a1572c2bec59ee52dd75be_114_0.png)

图 28 瓦片集

我们游戏引擎中的瓦片地图将由多个实体组成，每个实体附加一个瓦片组件。这使我们能够向瓦片添加更多组件，以实现更高级的游戏效果。例如，我们可以选择仅向某些瓦片添加碰撞体组件，仅在这些瓦片上处理碰撞。这将减少必须进行的碰撞测试次数，并为最终产品带来更好的性能。

注意：我始终使用 "struct" 而不是 "class"，因为我只是喜欢结构体。它们让我想起 C 语言。如果你愿意，可以随意使用类。唯一的区别是，结构体定义的成员变量和函数默认为公共。

engine/src/assets/tilemap.h
```cpp
#pragma once
#include "asset.h"

namespace fuse {
struct tileset {
    std::set<asset_id> tilesets;
    int col_count = 0;
    int row_count = 0;
    int tilesize = 0;
};

struct tilemap_asset : asset {
    FUSE_INLINE tilemap_asset() = default;
    tilemap instance;
};
}
```

瓦片地图还应该能够组合多个瓦片集来创建场景。这就是我们使用 std::set 来存储所有瓦片集的原因。同样重要的是要知道瓦片的单位大小，因为瓦片地图本质上只是一个网格。

## 资源注册表

现在我们已经定义了所有资源类型，需要创建一个资源注册表来跟踪添加到游戏引擎中的所有资源。接下来是一个代码片段，展示了资源注册表的定义方式。

get() 函数用于使用 asset_id 和类型从注册表中检索特定资源。所有资源都存储在成员变量 _data 中，它是一个资源指针的 std::vector 映射。

要检索资源，我们首先检查该特定资源类型是否有可用的数组。我们通过检查资源的 typeid 是否在映射中可用来完成此操作。如果没有可用的数组，我们直接返回 NULL。但如果找到了数组，我们将继续搜索传入参数的 id 的资源。下一个函数是 get_id()，它将资源名称作为参数，将类型名称作为模板参数。该函数将搜索资源并返回其 asset_id。

我们还希望能够向注册表中添加资源，因为有些资源（如瓦片地图和动画）并非最初从源文件加载，而纹理、字体和音频则是。这就是我们拥有 add() 函数的原因。

如果你仔细查看我们定义的所有资源类型，会发现它们都有一个默认构造函数。这是为了确保 add() 函数可以创建该资源的默认版本。

engine/src/assets/registry.h
```cpp
#pragma once
#include "font.h"
#include "audio.h"
#include "tilemap.h"
#include "texture.h"
#include "animation.h"
#include "core/typeid.h"

namespace fuse {
struct asset_registry {
    FUSE_INLINE void clear() {
        for(auto& [_, list] : _data) {
            for(auto a : list) { FUSE_DELETE(a); }
        }
        _data.clear();
    }
    template <typename T>
    FUSE_INLINE T* get(asset_id id) {
        FUSE_STATIC_ASSERT(std::is_base_of<asset, T>::value);
        const auto type = type_id<T>();
        if(!_data.count(type)) { return NULL; }
        for(auto& asset : _data.at(type)) {
            if(asset->id == id) { return static_cast<T*>(asset); }
        }
        return NULL;
    }
    template <typename T>
    FUSE_INLINE T* get(const std::string& name) {
        asset_id id = get_id(name);
        FUSE_STATIC_ASSERT(std::is_base_of<asset, T>::value);
        const auto type = type_id<T>();
        if(!_data.count(type)) { return NULL; }
        for(auto& asset : _data.at(type)) {
            if(asset->id == id) { return static_cast<T*>(asset); }
        }
        return NULL;
    }
    template <typename T>
    FUSE_INLINE asset_id get_id(const std::string& name) {
        FUSE_STATIC_ASSERT(std::is_base_of<asset, T>::value);
        const auto type = type_id<T>();
        if (!_data.count(type)) { return INVALID_ID; }

        for (auto& asset : _data.at(type)) {
            if (!asset->name.compare(name)) { return asset->id; }
        }
        return INVALID_ID;
    }

    template <typename T>
    FUSE_INLINE T* add(const std::string& name) {
        auto asset = new T();
        asset->name = name;
        _data[type_id<T>()].push_back(asset);
        return asset;
    }

private:
    std::unordered_map<asset_typeid, std::vector<asset*>> _data;
};
}
```

## engine/src/ecs/scene.h

```cpp
#pragma once
#include "assets/registry.h"

// ...

FUSE_INLINE void start() {
    auto frame1 = _assets.add<texture_asset>("frame1");
    auto frame2 = _assets.add<texture_asset>("frame2");
    auto anim = _assets.add<animation_asset>("test");

    anim->instance.frames.push_back(frame1->id);
    anim->instance.frames.push_back(frame2->id);
    anim->instance.speed = 200;
}

for (auto& sys : _systems) { sys->start(); }
}

private:
std::vector<ecs::system*> _systems;
SDL_Renderer* _renderer = NULL;
ecs::registry _registry;
asset_registry _assets;
};
```

在这种情况下，你必须做三件关键事情：包含资源注册表的头文件，在资源注册表中创建名为 "_assets" 的成员变量，并按上述所示修改 start() 函数。我们只是向注册表添加一个动画资源，以及两个将用作动画帧的纹理资源。

**编译、运行并使用调试器** 以检查一切是否按预期工作。你也可以打印出某些值，看它们是否符合你的预期。我们将在即将到来的章节中了解如何从文件加载纹理、字体和音频资源。

为了让你的 ecs::system 访问我们在场景中刚刚创建的资源注册表，请按下面所示更新你的系统。当我们开始添加精灵渲染器和动画器等系统时，这一点将很重要。

engine/src/ecs/system.h
```cpp
#pragma once
#include "entity.h"
#include "assets/registry.h"

namespace fuse::ecs {
struct system {
    FUSE_NO_INLINE virtual ~system() = default;

    FUSE_NO_INLINE void prepare(registry* rg, SDL_Renderer* rd, asset_registry* as) {
        this->rg = rg;
        this->renderer = rd;
        this->_assets = as;
    }

    template<typename T>
    FUSE_NO_INLINE auto view() {
        std::vector<entity> entities;
        for (auto& e : _registry->view<T>()) {
            entities.push_back(entity(e, _registry));
        }
        return entities;
    }

    FUSE_NO_INLINE virtual void update(float) {}
    FUSE_NO_INLINE virtual void start() {}

protected:
    SDL_Renderer* _renderer = NULL;
    asset_registry* _assets = NULL;
    registry* _registry = NULL;
};
};
```

你还必须确保更新场景的 register_system() 函数，以便在注册新系统时，该系统的 prepare() 函数会使用正确的参数列表被调用（参见下方代码）。

engine/src/scene/scene.h
```cpp
template <typename T>
FUSE_INLINE void register_system() {
    FUSE_STATIC_ASSERT(std::is_base_of<ecs::system<T>>::value);
    auto new_system = new T();
    new_system->prepare(&registry, &renderer, &assets);
    this->_systems.push_back(new_system);
}
```

