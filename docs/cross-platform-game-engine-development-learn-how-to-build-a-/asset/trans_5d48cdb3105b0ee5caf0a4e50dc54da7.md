

内存堆（Heap）上存储所有类型的对象。这意味着我们的数据不会在内存中连续存储。当你要求计算机在内存的特定地址查找某样东西时，它不仅会复制你要求的内容，还会复制你要求的内容周围的其他数据，并将它们全部存储在缓存内存中。因此，下次你要求其他东西时，计算机会直接从缓存中获取，而不是再次从 RAM 中获取。数据在内存中不连续存储这一事实大幅降低了 CPU 缓存的使用率，导致性能下降。

## 面向组件设计

下图展示了如何构建面向组件的设计。如你所见，每个游戏对象都将拥有一个组件列表，用于定义其行为。所有类似 Transform、Sprite 等组件都将继承一个名为 Component 的抽象类。

这种技术无法解决面向对象设计中内存和 CPU 缓存使用的问题，但它去除了虚函数的虚拟查找表，并提供了能够让老板同时也是玩家的能力，因为成为玩家或老板仅仅是添加或移除组件的问题。这将比面向对象设计表现更好。

![](img/2763810ed0a1572c2bec59ee52dd75be_89_0.png)

## 数据导向设计

数据导向设计听起来更合理，因为它提供了连续的内存布局、没有虚拟查找表以及更好的 CPU 缓存使用率。这种设计也称为实体-组件（EC）设计。下图描述了 EC 设计中最关键的部分。

![](img/2763810ed0a1572c2bec59ee52dd75be_90_0.png)

### 图 24 数据导向设计

每个游戏对象都由一个数字表示。该数字用于知道哪个组件属于该实体。你可以看到，所有实体中相同类型的所有组件都以连续的方式存储在一起。这将对 CPU 缓存产生积极影响。许多游戏引擎使用这种设计，因为它提供可靠的性能，且维护也不困难。

## ECS 架构

尽管 ECS 设计因其高性能以及在维护、内存和 CPU 缓存使用方面的易用性而闻名，但它缺乏特定的实现方法。我通常将实现 ECS 的方法分为两类：纯 ECS 和混合/混杂 ECS。

在纯 ECS 中，组件没有逻辑。只有系统持有用于更新组件的逻辑。混合 ECS 允许组件拥有用于自行更新的逻辑。

我们将在本书中构建一个纯 ECS。

![](img/2763810ed0a1572c2bec59ee52dd75be_91_0.png)

使 ECS 设计与数据导向设计不同的是，实体、组件和系统全部被分离。实体只是一个唯一标识符（数字），代表场景中的特定游戏对象。它通常是一个 32 位或 64 位无符号整数。组件是一个简单的结构，存储逻辑所需的所有数据。系统针对拥有特定组件集合（签名）的所有实体并更新它们的组件。

### ECS 的优势：

- ECS 是一种用户友好的多线程方法，因为每个系统可以分配给特定线程。
- 代码更短且更不复杂。
- 轻松集成脚本语言。
- 使单元测试和模拟变得容易。
- 新功能可以轻松实现。

### ECS 的劣势

- 未定义标准实现方法。
- 正确实现困难且容易被滥用
- 大多数游戏开发者不太熟悉。

你可以在这里 [16] 和这里 [9] 了解更多关于 ECS 的信息。我们现在有足够的理论知识。那么，让我们实现自己的自定义 ECS。

## 实现

![](img/2763810ed0a1572c2bec59ee52dd75be_93_0.png)

上图是一个图表，展示了你的引擎文件夹树目前应该是什么样子。请确保创建所有标记为红色的内容。文件夹：**components/** 是我们将创建组件的地方。所有系统都将在文件夹 **systems/** 中创建。所有系统都将继承 **ecs::system**。

```
engine/src/ecs/ecs.h
```

```cpp
#pragma once
#include "core/typeid.h"

namespace fuse::ecs {
    using entityid = size_t;
    using componentid = uint32_t;
    using signature = std::set<uint32_t>;
    using entitylist = std::set<entityid>;

    // component array interface
    struct array_instance {
        FUSE_NOLINE virtual ~array_instance() = default;
        virtual void erase(entityid) = 0;
    };

    // component array's data entry
    template<typename T> struct array_entry {
        FUSE_NOLINE array_entry(entityid e, const T& d): entity(e),
        data(d) {}
        FUSE_NOLINE operator entityid() const { return entity; }
        entityid entity = INVALID_ID;
        T data;
    };

    // component array
    template<typename T>
    struct component_array : array_instance {
        FUSE_NOLINE T& push(entityid e, const T& data) {
            if (exists(e)) { return get(e); }
            _data.push_back(array_entry(e, data));
            return _data.back().data;
        }

        FUSE_NOLINE void erase(entityid e) {
            auto it = std::find(_data.begin(), _data.end(), e);
            if (it != _data.end()) { _data.erase(it); }
        }

        FUSE_NOLINE bool exists(entityid e) {
            return std::find(_data.begin(), _data.end(), e) != _data.end();
        }

        FUSE_NOLINE T& get(entityid e) {
            FUSE_ASSERT(exists(e) && "entity out of range!");
            return (*std::find(_data.begin(), _data.end(), e)).data;
        }

        private:
            std::vector<array_entry<T>> _data;
    };
}
```

我们的实体组件系统所需的一些基本元素的定义都包含在头文件 ecs.h 中。我们想知道哪些组件以及有多少个组件属于一个实体。这就是为什么我们有签名，它只不过是一组组件 ID。每个实体都会分配一个签名，该实体由名为 entityid 的 64 位无符号整数表示。该元素是 array_entry。这个模板结构存储类型为 "T" 的组件及其所属的实体。我们定义了一个转换为 entityid 的强制转换运算符，因为在 component_array 中搜索组件时，我们将简单地使用 entityid 来搜索组件。这个结构也表示组件将如何在 component_array 中存储。由于我们希望以缓存友好的方式在内存中存储组件，因此必须创建一个自定义组件数组来存储它们。每种组件类型都将有自己的组件数组。这就是为什么我们创建了一个名为 array_instance 的接口，目前它只有一个名为 erase() 的虚函数。然后我们使用该接口创建一个名为 component_array 的模板结构，它以要存储的组件类型作为模板参数。如果你仔细观察，会发现这个组件数组只不过是 C++ std::vector 容器的包装器。它包含 push、remove 和 get 等函数，就像标准数组一样。

engine/src/ecs/registry.h

```cpp
#pragma once

#include "ecs.h"

namespace fuse::ecs {
struct registry {
    FUSE_INLINE void clear() {
        for (auto& [_, a] : _components) { FUSE_DELETE(a); }
        _components.clear();
        _signatures.clear();
        _nextid = INVALID_ID;
    }

    FUSE_INLINE entityid add_entity() {
        entityid entity = _nextid++;
        _signatures[entity] = signature();
        return entity;
    }

    FUSE_INLINE void destroy(entityid e) {
        for (auto& [_, a] : _components) {
            a->erase(e);
        }
        _signatures.erase(e);
    }

    FUSE_INLINE bool is_alive(entityid e) {
        return _signatures.count(e);
    }

    template <typename T> FUSE_INLINE entitylist view() {
        entitylist list;
        for (auto& [entity, sig] : _signatures) {
            if (sig.count(type_id<T>())) {
                list.insert(entity); continue;
            }
        }
        return list;
    }

    template <typename T>
    FUSE_INLINE T& get_component(entityid e) {
        FUSE_ASSERT(_signatures.count(e) && "out of range!");
        return get_component_array<T>()->get(e);
    }

    template <typename T, typename... Args>
    FUSE_INLINE T& add_component(entityid e, Args&&... args) {
        FUSE_ASSERT(_signatures.count(e) && "out of range!");
        T data(std::forward<Args>(args)...);
        _signatures[e].insert(type_id<T>());
        return get_component_array<T>()->push(e, data);
    }

    template <typename T>
    FUSE_INLINE void remove_component(entityid e) {
        _signatures.at(e).erase(type_id<T>());
        get_component_array<T>()->erase(e);
    }

    template <typename T>
    FUSE_INLINE bool has_component(entityid e) {
        return _signatures.count(e) && _signatures.at(e).count(type_id<T>());
    }

    template <typename T>
    FUSE_INLINE component_array<T>* get_component_array() {
        component_id type = type_id<T>();
        if (_components.count(type)) {
            return static_cast<component_array<T>*>(_components.at(type));
        }
        auto array = new component_array<T>();
        _components[type] = array;
        return array;
    }

private:
    std::unordered_map<component_id, array_instance*> _components;
    std::unordered_map<entityid, signature> _signatures;
    entityid _next_id = INVALID_ID;
};
}
```

