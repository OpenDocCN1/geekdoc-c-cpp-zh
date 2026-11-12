

```cpp
#pragma once
#include "script_instance.h"

namespace fuse {
struct player_controller : script_instance {
    FUSE_INLINE void on_collision(ecs::entity e) {
        auto& sp = get_component<ecs::sprite_component>();
        sp.sprite = get_asset<texture_asset>("dead")->id;
        get_component<ecs::collider_component>().disabled = true;
        get_component<ecs::rigid_body_component>().disabled = true;
    }

    FUSE_INLINE void on_update(float dt) {
        auto& rb = get_component<ecs::rigid_body_component>();
        if (inputs::is_key(SDL_SCANCODE_SPACE)) {
            rb.body.set_force_y(-1000.0f);
        }
        else {
            rb.body.set_force_y(0.0f);
        }
    }
};
}
```

为了让飞机保持在空中，我们使用空格键。当按下空格键时，会向飞机施加一个向上的推力，以抵御使其下坠的重力。玩家还需要响应与水管和地面的碰撞。

我们正在实现 "on_update" 和 "on_collision" 两个函数。更新函数会在每次按下空格键时向飞机施加推力。如果玩家与水管或地面发生碰撞，我们会将其精灵更换为显示玩家已死亡的另一个精灵。然后我们禁用刚体和碰撞器组件，以防止系统继续更新它们。

注意：你也可以使用鼠标按钮代替空格键。

## 添加玩家实体

![](img/2763810ed0a1572c2bec59ee52dd75be_198_0.png)

用于玩家。左侧的第一个精灵用于飞机飞行时，第二个用于飞机坠毁时。

让我们返回场景并添加一个玩家实体。以下是代码片段。

```
FUSE_INLINE void start() {
 // ...
 // // player
 auto & player = add_entity("player");
 auto & ps = player.add_component<ecs::script_component>();
 ps.bind<player_controller>();
 ps.name = "player_controller";
 auto & tr = player.add_component<transform_component>();
 tr.translate = vec2f({126, 360});
 tr.scale = vec2f(0.5f);
 auto & rb = player.add_component<rigidbody_component>();
 rb.body.gravity_scale = 25.0f;
 player.add_component<sprite_component>().sprite = fly_id;
 auto & cl = player.add_component<collider_component>();
 cl.collider = { 0, 0, 58, 38 };
 // start systems
 for (auto & sys : _systems) { sys->start(); }
}
```

我们正在添加一个带有脚本组件的实体。迄今为止我们还没有为脚本组件的名称用过任何用途，但设置其值很重要，因为我们稍后将使用它来序列化和反序列化场景。序列化将在下一章中实现。

玩家还有一个刚体和一个碰撞器组件。盒形碰撞器的大小适合我使用的精灵。因此，如果你为飞机使用不同的精灵，请务必设置自己的值。我们正在获取玩家的变换组件以设置其初始位置，基本上是屏幕中心。我们必须增加重力缩放值，以增加重力对飞机的影响。

如果你编译并运行代码，就可以使用空格键让飞机保持在空中。但如果撞到地面，玩家精灵会改变，并且它将停止移动。

## 图 41 玩家控制

![](img/2763810ed0a1572c2bec59ee52dd75be_199_0.png)

飞机坠毁时我们也将停止地面滚动运动。但让我们先添加一个水管生成器。

## 水管生成器

水管生成器也是一个实体。它将在特定的时间间隔内生成水管，以便玩家躲避。由于水管将在运行时生成，我们需要在生成器上附加一个脚本来持续生成水管，并确保它们在屏幕外被销毁。

![](img/2763810ed0a1572c2bec59ee52dd75be_199_1.png)

```
engine/src/scripts/pipe_spawner.h
#pragma once
#include "script_instance.h"

namespace fuse {
struct pipe_spawner : script_instance {
    FUSE_INLINE void on_update(float dt) {
        // ... coming next
    }

    FUSE_INLINE void spawn_pipe(float x, float y) {
        // ... coming next
    }

    FUSE_INLINE void update_pipes() {
        // ... coming next
    }

private:
    std::vector<ecs::entity> pipes;
    bool game_over = false;
    float time = 0.0f;
    int score = 0;
};
}
```

以上是“pipe_spawner”脚本的简单定义。我们将在片刻之后逐一介绍每个成员函数的实现。

在成员变量部分，我们定义了一些重要变量。我们有一个名为 "pipes" 的数组，它将保存所有创建的水管列表。这很重要，因为我们希望在水管超出屏幕视口时将其销毁。

实现此目的的另一种方法是在创建水管时创建一个脚本并将其附加到水管上。该脚本将每帧检查水管的当前位置，并在其超出边界时将其销毁。但将脚本附加到生命周期较短的对象（如粒子）上不是良好做法，因为创建脚本需要堆分配，当活动脚本过多时可能会导致性能问题。

我们有一个名为“game_over”的布尔值，用于告诉我们飞机是否已坠毁。我们将使用“time”来知道何时生成新水管，最后我们有“score”。

```
engine/src/scripts/pipe_spawner.h
// ...
FUSE_INLINE void spawn_pipe(float x, float y) {
    auto pipe = add_entity();
    auto& tr = pipe.get_component<ecs::transform_component>();
    tr.translate = vec2f(x, y);

    // add rigid body
    auto& rb = pipe.add_component<ecs::rigidbody_component>();
    rb.body.gravity_scale = 0.0f;
    rb.body.velocity.x = -100.0f;

    // add sprite
    auto pipe_sprite = get_asset<texture_asset>("pipe");
    auto& sp = pipe.add_component<ecs::sprite_component>();
    sp.flip = (y < 0) ? SDL_FLIP_NONE : SDL_FLIP_VERTICAL;
    sp.sprite = pipe_sprite->id;

    // add collider
    auto& cl = pipe.add_component<ecs::collider_component>();
    cl.collider = {
        tr.translate.x,
        tr.translate.y,
        (float)pipe_sprite->instance.width,
        (float)pipe_sprite->instance.height
    };
    pipes.push_back(pipe);
}
// ...
```

以上是用于生成水管的水管生成器脚本成员函数。它将必须生成水管的位置作为参数。
正如你所见，我们正在创建一个带有刚体、精灵和碰撞器组件的实体。因为我们总是需要从上到下创建一个水管，以及从下到上创建另一个水管，所以我们检查 y 轴上的位置是否小于零，以确定精灵是否需要垂直翻转。
盒形碰撞器的大小与精灵大小相同。
创建水管只需要做这些。让我们看看函数

## "update_pipes" 的工作原理。

```
engine/src/scripts/pipe_spawner.h

// ...
FUSE_INLINE void update_pipes() {
    auto it = pipes.begin();
    while (it != pipes.end()) {
        // remove dead pipe
        auto& pipe = (*it);
        if (!pipe.is_alive()) {
            it = pipes.erase(it);
            continue;
        }
        it++;
    }
}
// ...
```

"update_pipes" 函数的主要工作是遍历水管列表，检查是否有水管超出边界并将其销毁。这非常重要，因为如果没有它，每次创建一对水管时内存大小都会增加。使用 while 循环是因为我们希望在遍历数组的同时能够从中删除数据。

在查看“on_update”函数之前，我希望你在 math 文件夹中定义以下函数，因为它将用于生成随机数。

```
engine/src/math/random.h
#pragma once
namespace fuse::math {
    FUSE_INLINE int random(int min, int max) {
        static bool first = true;
        if (first) {
            srand(time(NULL)); // seeding for the first time only!
            first = false;
        }
        return min + rand() % ((max + 1) - min);
    }
}
```

