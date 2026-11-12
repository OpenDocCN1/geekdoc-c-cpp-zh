
对模拟的影响。

![](img/2763810ed0a1572c2bec59ee52dd75be_163_0.png)

图 35 刚体测试

就这样，我们有了一个用于模拟刚体的系统。但我们仍然有一个问题。所使用的增量时间（delta time）值不应是恒定的，因为增量时间强烈依赖于正在使用的计算机的性能。我们现在使用的值在 PlayStation 或旧计算机上不会相同。这就是为什么我们必须通过向引擎添加适当的增量时间计算来解决这个问题。

## 增量时间

在游戏编程和计算机图形学中，增量时间描述了一个概念，它确保游戏循环中进程的速度与硬件无关。增量时间描述了前一帧与当前渲染帧之间的时间差。增量时间的概念被引入以解决早期计算机游戏中的一个问题：游戏运行速度取决于处理器的速度，因此有时在比游戏开发者预期更快的处理器上不再可玩。[22]

## 基于帧率的游戏

这类游戏不是基于时间，而是基于所使用计算机的帧率。在 30 FPS 机器上移动一个对象，在 60 FPS 机器上运行速度会减半。依赖帧率的游戏会严重影响游戏体验，因为游戏的流程将取决于用于运行游戏的设备的帧率。

## 基于时间的游戏

基于时间的游戏在不同机器上具有相似的行为（运动、动画和物理），无论帧率如何。这意味着，在“基于时间的”游戏中移动的对象将以相同的速率移动，无论计算机速度如何。

当目标是设计多平台游戏时，会使用这种技术。这也是我们希望在引擎中使用它的原因。

- **engine/src/core/application.cpp**

```cpp
#include "pch.h"
#include "inputs.h"
#include "ecs/scene.h"
#include "application.h"
#include "events/system.h"

namespace fuse {
static bool is_running = true;
static float deltatime, last_tick;

FUSE_INLINE bool on_quit(const quit_event&) {
    return is_running = false;
}

FUSE_INLINE void compute_deltatime() {
    deltatime = get_ticks() - last_tick;
    if (deltatime > MAX_DELTATIME) {
        deltatime = MAX_DELTATIME;
    }
    last_tick = get_ticks();
}

FUSE_API void run_application(const app_config& config) {
    // ...

    last_tick = get_ticks();

    while (is_running) {
        compute_deltatime();
        inputs::dispatch_events();
        SDL_RenderClear(renderer);
        scene->update(deltatime);
        SDL_RenderPresent(renderer);
    }

    // ...
}
}
```

在 application.cpp 文件中添加上述高亮的行。如您所见，函数 compute_deltatime() 将通过计算当前帧与上一帧之间的时间差来计算每一帧的 delta 值。为了确保增量时间的值不会过高，我们始终检查其值是否高于某个阈值“MAX_DELTATIME”，在本例中该值为 0.05f。

如果您现在将增量时间的值传递给场景的 update 函数，将获得基于时间的物理模拟。如果您在控制台中打印增量时间的值，将得到类似下面的值。

```
[info] 0.016000
[info] 0.017000
[info] 0.017000
```

请记住，这取决于您的计算机性能。因此，您的增量时间可能与上面的不同。

仅仅让物体因重力下落是不够的。我们还希望它们能响应碰撞。

## 碰撞处理

2D 碰撞由碰撞图形的类型决定。例如，我们有矩形对矩形碰撞或圆形对圆形碰撞。通常，我们会在实体周围有一个名为“盒子碰撞器”的简单矩形形状。这种技术并不完美，但在性能和功能之间提供了特别好的比率。

![](img/2763810ed0a1572c2bec59ee52dd75be_167_0.png)

图 36 碰撞

只有当两个碰撞器重叠时，才能检测到碰撞。这种碰撞检测不是像素级精确的。碰撞后发生什么由我们决定。

我们将创建一个碰撞器组件，以确保只有带有碰撞器组件的实体才能对碰撞做出反应。这一点很重要，因为它将减少碰撞测试的数量。

我们还将创建一个单独的碰撞处理系统，以保持代码整洁，因为这将使我们以后更容易添加脚本功能。

## 碰撞器组件

碰撞器组件也应添加到头文件 physics.h 中。以下是显示盒子碰撞器组件定义的代码片段。

engine/src/ecs/components/physics.h

```cpp
#pragma once
#include "physics/cs/rigidbody2.h"

namespace fuse::ecs {
struct rigidbody_component {
FUSE_INLINE rigidbody_component(const rigidbody_component&) = default;
FUSE_INLINE rigidbody_component() = default;
bool disabled = false;
rigidbody2 body;
};

struct collider_component {
FUSE_INLINE collider_component(const collider_component&) = default;
FUSE_INLINE collider_component() = default;
SDL_FRect collider = { 0.0f, 0.0f, 64.0f, 64.0f };
bool disabled = false;
};
}
```

碰撞器组件只是一个使用 SDL_FRect 定义的矩形。它还有一个布尔值，用于指示碰撞器是否处于活动状态。

## 碰撞系统

与其他系统相比，碰撞系统将实现 start 函数，因为我们需要确保盒子碰撞器的位置与实体的初始位置对齐。
下一个代码片段展示了碰撞系统的实现方式。start 函数会获取所有带有碰撞器组件的实体，并将它们的位置设置为所属实体的变换位置。
在 update 函数中，我们每帧重复该过程，同时检查是否发生了碰撞。要检测碰撞，我们只需检查两个矩形图形之间是否存在交集。您可以在 check_collision() 函数中看到这一点。
目前，我们只是在两个实体碰撞时在控制台打印一条消息。为了防止对象与自身碰撞，我们始终检查当前碰撞中涉及的实体是否不相等。

engine/src/ecs/systems/collision_system.h

```cpp
#pragma once
#include "ecs/system.h"

namespace fuse::ecs {
struct collision_system: system {
    FUSE_INLINE void start() {
        for (auto& e : view<collider_component>()) {
            auto& tr = e.get_component<transform_component>();
            auto& col = e.get_component<collider_component>();
            col.collider.x = tr.translate.x;
            col.collider.y = tr.translate.y;
        }
    }

    FUSE_INLINE void update(float) {
        // get entity list
        auto entities = view<collider_component>();

        for (auto& e : entities) {
            auto& tr = e.get_component<transform_component>();
            auto& c1 = e.get_component<collider_component>();

            // update box collider offset
            c1.collider.x = tr.translate.x;
            c1.collider.y = tr.translate.y;

            // continue if disabled
            if (c1.disabled) { continue; }

            // check collision with others
            for (auto& o : entities) {
                if (o == e) { continue; }
                auto& c2 = o.get_component<collider_component>();

                if (check_collision(c1.collider, c2.collider)) {
                    FUSE_INFO("collision: %d -> %d", e.id(), o.id());
                }
            }
        }
    }

private:
    bool check_collision(const SDL_FRect& a, const SDL_FRect& b) {
        return ((a.x < b.x + b.w) && (a.x + a.w > b.x) &&
                (a.y < b.y + b.h) && (a.y + a.h > b.y));
    }
};
}
```

让我们在场景中快速测试一下，看看这是否有效。

engine/src/ecs/scene.h

```cpp
FUSE_INLINE void start() {
 // load sprite
 auto sp1 = _assets.load_texture("assets/obj1.png", "", _renderer);
 auto sp2 = _assets.load_texture("assets/obj2.png", "", _renderer);

 // add tilemap entity
 auto e1 = add_entity("entity1");
 e1.add_component<rigid_body_component>().body.set_force_x(-50);
 e1.get_component<transform_component>().translate.x = 500;
 e1.add_component<sprite_component>().sprite = sp1 >> d;
 e1.add_component<collider_component>();

 auto e2 = add_entity("entity2");
 e2.add_component<rigid_body_component>().body.set_force_x(50);
 e2.add_component<sprite_component>().sprite = sp2 >> d;
 e2.add_component<collider_component>();

 // start systems
 for (auto& sys : _systems) { sys->start(); }
}

FUSE_INLINE void update(float dt) {
 for (auto& sys : _systems) { sys->update(dt); }

 // render box colliders
 SDL_SetRenderDrawColor(_renderer, 0, 0, 0, 255);
 for (auto& e : _registry.view<collider_component>()) {
 auto& c = _registry.get_component<collider_component>(e);
 SDL_RenderDrawRectF(_renderer, &c.collider);
 }

 SDL_SetRenderDrawColor(_renderer, 255, 255, 255, 255);
}
```

注意：不要忘记在构造函数中注册碰撞系统。

我们只是创建两个实体，每个实体都带有刚体组件和碰撞器组件。我们将每个刚体的重力比例保持为零，以确保它们不会因重力而下落。第二个实体距离第一个实体 500 米（像素），它们都以大约 50 m/s 的速度相互移动。

为了避免由于碰撞器位置与对象位置不同而导致的不一致，我们确保系统已启动。这将强制
