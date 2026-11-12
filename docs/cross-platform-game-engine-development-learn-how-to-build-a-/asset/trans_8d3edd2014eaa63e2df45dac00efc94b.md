

游戏可在 GitHub 仓库中找到。

## 开始使用

我们要做的第一件事是更改游戏配置。因此，请确保像下面所示更新应用程序的配置。

```
game/src/game.cpp

#include <core/entry.h>
fuse::app_config fuse::create_application() {
    fuse::app_config config;
    config.title = "Flappy Plane";
    config.version = "0.0.1";
    config.width = 380;
    config.height = 720;
    return config;
}
```

如您所见，我们已更改了应用程序窗口的宽度、高度和标题。

## 脚本实例更新

在上一章中，我们通过使用键盘移动实体来测试脚本系统。但是，如果我们想要访问某些资产呢？或者假设我们想要在场景中查找特定实体，等等。例如，我们希望在玩家死亡时更改其精灵。这正是我们在这里想要做的。我们希望向脚本实例添加更多成员函数，以允许访问资产注册表。

```
engine/src/scripts/script_instance.h
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

第一个函数“destroy”可用于删除当前持有脚本的实体。第二个函数“find_entity”使用作为参数提供的名称查找实体。最后，我们有一个方法，它接受一个字符串、一个模板类型并返回资产指针。此函数将搜索类型为“T”且名称作为参数提供的资产。

## 添加背景精灵

游戏场景的背景只不过是一个附加了精灵组件的实体。接下来是一个代码片段，展示如何将背景实体添加到场景中。

- engine/src/ecs/scene.h

```
FUSE_INLINE void start() {
  // load player sprites
  auto dead = _assets.load_texture("assets/dead.png", "dead",
                                     _renderer);
  auto fly = _assets.load_texture("assets/fly.png", "fly", _renderer);
  // load pipe sprite
  auto pipe = _assets.load_texture("assets/pipe.png", "pipe",
                                   _renderer);
  // load bg texture
  auto ground = _assets.load_texture("assets/ground.png",
                                     "ground", _renderer);
  auto background = _assets.load_texture("assets/bg.png", "bg",
                                         _renderer);
  // load text font
  auto font = _assets.load_font("assets/font.ttf", "font", 30);

  // background
  auto bg = add_entity("background");
  bg.add_component<sprite_component>().sprite = background->id;

  // start systems
  for (auto& sys : _systems) { sys->start(); }
}
```

![](img/2763810ed0a1572c2bec59ee52dd75be_192_0.png)

上面的代码片段展示了制作游戏所需的一些资产是如何加载到资产注册表中的，以及如何通过带有精灵组件的实体将背景图像添加到场景中。我们确保每个资产都有有效的名称，以便以后可以使用该名称来搜索它们。

目前，我们不加载任何音频，但会在合适的时候进行。如果您编译代码，将能够看到如下图所示渲染的背景图像。

![](img/2763810ed0a1572c2bec59ee52dd75be_193_0.png)

图 39 地面精灵

## 添加地面精灵

我们想要添加地面以防止飞机永远下落。地面将带有一个盒形碰撞器，以便与飞机进行碰撞检测。它还将进行动画处理，以产生连续平移运动的感觉。

![](img/2763810ed0a1572c2bec59ee52dd75be_193_1.png)

图 40 地面平移运动

由于游戏必须持续到玩家存活，我们必须使此动画无限循环。我们可以通过在帧动画中简单地从一帧切换到下一帧来实现相同的效果。但是，因为我不是艺术家，而且我们想看看脚本系统的潜力，我们将简单地使用脚本来实现。

```
engine/src/scripts/scrolling_ground.h
#pragma once
#include "script_instance.h"
namespace fuse {
struct scrolling_ground : script_instance {
FUSE_INLINE void on_start() {
width = get_asset<texture_asset>("ground")->instance.width;
}
FUSE_INLINE void on_update(float dt) {
auto& tr = get_component<ecs::transform_component>();
if(tr.translate.x + width < 380) {
tr.translate.x = 0.0;
}
}
private:
float width;
};
}
```

我们在此脚本中实现了一个启动函数和一个更新函数。启动函数将检索地面精灵的宽度。这一点很重要，因为我们将使用它来检查精灵的当前位置加上其高度是否小于窗口的宽度。如果是这种情况，我们就会知道需要将地面精灵移回其初始位置。在“on_update”函数中使用的“380”只不过是窗口的宽度。

我们本可以将游戏配置作为参数传递给“script_instance”构造函数，以便通过调用父函数获取宽度，但那将是你的工作。

## 添加地面实体

下面是展示如何将地面实体添加到场景中的代码片段。请务必相应地更新场景的启动函数。

```
engine/src/ecs/scene.h
```cpp
FUSE_INLINE void start() {
// load player sprites
auto dead = _assets.load_texture("assets/dead.png", "dead",
_renderer);
auto fly = _assets.load_texture("assets/fly.png", "fly", _renderer);
// load pipe sprite
auto pipe = _assets.load_texture("assets/pipe.png", "pipe",
_renderer);
// load bg texture
auto ground = _assets.load_texture("assets/ground.png",
"ground", _renderer);
auto background = _assets.load_texture("assets/bg.png", "bg",
_renderer);
// load text font
auto font = _assets.load_font("assets/font.ttf", "font", 30);

// background
auto bg = add_entity("background");
bg.add_component<sprite_component>().sprite = background->id;

// ground
auto gd = add_entity("ground");
auto& gds = gd.add_component<ecs::script_component>();
gds.bind<scrolling_ground>();
gds.name = "scrolling_ground";
auto& gd_tr = gd.get_component<transform_component>();
gd_tr.translate = vec2f(0.0f, 620);
gd.add_component<rigidbody_component>().body.velocity.x = -100.0f;
auto& gd_sp = gd.add_component<sprite_component>().sprite = ground->id;
auto& gd_cl = gd.add_component<collider_component>();
gd_cl.collider = { 0, 0, (float)ground->instance.width,
(float)ground->instance.height };

// start systems
for (auto& sys : _systems) { sys->start(); }
}
```
```

![](img/2763810ed0a1572c2bec59ee52dd75be_196_0.png)

我们首先添加之前描述的脚本，然后希望确保精灵位于正确的位置。这就是为什么我们检索转换组件并设置其位置。

平移运动由刚体系统处理。这就是为什么我们将刚体的速度设置为“-100”。我们还添加了一个与精灵大小完全相同的盒形碰撞器。

这就是在游戏中实现滚动地面所需的全部操作。因此，如果您编译并运行，将看到一个带有背景颜色和滚动地面的窗口，如下图所示。

## 玩家控制器脚本

下面是玩家控制器脚本的代码片段。

```
engine/src/scripts/player_controller.h
```

