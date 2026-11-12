

碰撞系统用于初始化所有碰撞体的位置。
出于调试目的，我们想要渲染盒形碰撞体的形状。为此，我们只需使用 SDL 内置函数来渲染 SDL_FRect。

如果你编译并运行代码，你将看到两个带有盒形碰撞体的对象向相反方向移动，如下图所示。

![](img/2763810ed0a1572c2bec59ee52dd75be_171_0.png)

当它们发生碰撞时，终端中将打印以下消息。

```
[info] collision: 2 -> 1
[info] collision: 1 -> 2
[info] collision: 2 -> 1
[info] collision: 1 -> 2
```

你可以在碰撞发生时执行其他操作，而不仅仅是在控制台打印一条消息，从而与碰撞系统进行实验。你可以将重力比例设置为非零值，以便在检测到碰撞时实体可以下落。

```
if (check_collision(c1.collider, c2.collider)) {
    auto& rb = e.get_component<rigidbody_component>();
    rb.body.gravity_scale = 0.5f;
}
```

## 结论

这个物理引擎对于游戏引擎来说是不够的。本书未涵盖许多其他模拟。但就目前而言，它所提供的功能足以制作一款好游戏。

使用 Box2D 这样的库是个聪明的主意，因为它在 2D 游戏行业中广为人知，并在 2D 物理模拟方面提供了更多功能。

注：如果你在自己的代码中遇到任何问题，欢迎从仓库克隆源代码。当前代码的版本位于名为“physics”的分支下。

## 第 12 章 原生脚本

## 原生脚本

迄今为止，本书一直在添加纹理、文本渲染、动画和物理模拟等功能，但我们仍然不太清楚如何利用这些功能来制作游戏。我们不想忘记，游戏引擎的主要目的是制作游戏，而不仅仅是将一堆功能集合在一起。

脚本正是为此而来。它将使我们能够利用迄今添加的所有功能来创建游戏。

脚本语言（也称为脚本语言）是一种用于运行时系统的编程语言，用于自动执行原本需要由人工操作员独立完成的进程。

脚本语言通常是解释型而非编译型。[26]

## 编译型和解释型脚本

从标题可以看出，我们将创建一个原生脚本系统。这意味着它将使用与引擎相同的编程语言，并且也是一个编译型而非解释型的脚本系统。这意味着脚本是作为引擎源代码的一部分编写的，并与引擎一起编译。与编译型脚本相比，解释型脚本效率稍低，但它提供了在运行时热重载而无需重启应用程序的能力。不过，创建这样的系统需要了解多种编程语言和内存布局，而这不是本书要尝试的。编译版本的优势在于其原生性，这意味着更好的性能和较低的复杂度。

下图展示了一个使用 C# 作为编程语言的解释型脚本系统示例。C# 是最广泛使用的脚本语言之一，因为它易于与 C++ 集成，并且易于理解。

![](img/2763810ed0a1572c2bec59ee52dd75be_175_0.png)

图 37 C# 脚本架构示例

Unity3D 和许多其他游戏引擎使用 C# 进行脚本编写。还有 Lua、Java、JavaScript 等其他语言。上图中的 C# 代码将被编译为动态共享库，该库可以在运行时链接到引擎，引擎将简单地调用脚本中的函数来执行开发者的任务。

虽然这个图看起来很简单，但将其组合在一起所需的努力可能比你想象的更多。这或许可以作为另一本书的好主题，但目前，让我们专注于原生脚本。

## 抽象脚本

由于将有许多脚本通过单个系统运行，我们必须以某种方式为所有脚本创建一种模式。我们希望所有脚本都具有某些函数，这样我们就可以调用它们而无需检查该函数是否存在。这就是为什么我们将使用虚函数和继承。本节将介绍创建一个核心类，所有脚本都将继承该类，并决定是否要实现虚函数的自己的版本。由于这个脚本系统与实体组件系统紧密相关，我们希望轻松访问注册表中实体的组件。这就是为什么我们将创建一个自定义实体对象，该对象可以访问注册表。该实体对象将在我们的脚本中用于操作实体。让我们先创建实体对象，其余部分就会更加清晰。

### 创建脚本实例

下一个代码片段展示了脚本实例的定义。请确保在引擎的文件夹树中创建相同的文件来更新它。如你所见，这是一个带有许多虚函数的抽象类。在成员变量部分，我们定义了一个实体 ID、一个指向资产注册表的指针和一个指向 ecs::registry 的指针。实体 ID 是带有脚本的游戏对象。指向资产注册表的指针很重要，因为我们希望在脚本中也能访问所有资产。

最上方是一个名为 script_props 的结构体，它只是我们定义的一个简单容器，用于保存初始化脚本实例所需的参数。我们有一组虚函数，可以在派生脚本中实现，以对实体执行自定义行为。init() 函数用于将成员变量设置为适当的值。

我们还在底部有一个 script_instantiator，它是一种 lambda 函数类型，用于实例化脚本实例。C++ 允许我们使用 lambda 表达式创建内联函数，这对于那些不会被重复使用且不值得命名的简短代码片段很有用。script_instantiator 函数返回一个指向脚本实例的指针，并以 script_props 作为参数。该参数将传递给脚本的 init() 函数以设置其成员变量。

```
engine/src/scripts/script_instance.h
```

```
#pragma once
#include "ecs/components/graphics.h"
#include "ecs/components/physics.h"
#include "ecs/components/common.h"
#include "ecs/entity.h"

#include "assets/registry.h"
#include "core/inputs.h"

namespace fuse {
struct script_props {
FUSE_INLINE script_props(ecs::entity_id e, ecs::registry* r,
asset_registry* a):
entity(e), registry(r), assets(a) {}
ecs::entity_id entity = INVALID_ID;
ecs::registry* registry = NULL;
asset_registry* assets = NULL;
};

struct script_instance {
FUSE_INLINE virtual ~script_instance() = default;

FUSE_INLINE void init(const script_props& props) {
this->registry = props.registry;
this->assets = props.assets;
this->entity = props.entity;
}

FUSE_INLINE virtual void on_collision(ecs::entity) {}
FUSE_INLINE virtual void on_update(float) {}
FUSE_INLINE virtual void on_destroy() {}
FUSE_INLINE virtual void on_start() {}

private:
ecs::entity_id _entity = INVALID_ID;
ecs::registry* _registry = NULL;
asset_registry* _assets = NULL;
};

// script allocator function type
using script_instantiator = std::function<script_instance*(const script_props&)>;
}
```

由于 registry 是私有成员变量，任何继承自 script_instance 的脚本都无法访问它。这意味着我们将无法访问实体的组件。

为了解决这个问题，我们将在此处将 add-、get-、remove 组件函数的几个实现添加为受保护的成员函数。因此，请在脚本实例结构体中添加以下代码片段。

### engine/src/scripts/script_instance.h

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

我们现在将能够轻松访问当前持有脚本的实体的所有有价值信息。add_entity() 函数将添加一个带有某些核心组件的新实体，并返回一个实体对象。

我们现在拥有创建脚本组件及其系统所需的一切。流程保持不变，我们先创建组件，然后创建系统，并测试一切是否协同工作。

