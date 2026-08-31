
# C++ 秘籍：如何使用最新 C++ 版本编写优秀代码

## 关于作者

Wayne Murphy 出于加拿大安大略省的布林普顿。他于 1987 年开启了他的第一份编程工作，在过去的多年里，曾在许多公司担任过多种角色。在过去的 20 年里，他一直在自己的公司 `Great Leap Forwards Inc` 提供咨询服务。

## 关于评审员

- **Maxim Chetruşca**：软件工程师，拥有十年的 C++ 经验，专注于实时、对延迟敏感的系统开发。
- **Kris Jusiak**：软件工程师，专精现代 C++ 开发、性能和质量。
- **Chetan Sachdeva**：技术爱好者，在 C++、Python、汽车、AR/VR 和 IoT 领域拥有 13 年以上的专业知识。

## 前言

`C++ Cookbook` 以“食谱”的形式带你了解所有最近的新特性。它展示了如何用通俗的语言使用每个新类或函数。这本书将帮助读者跟上最新的 C++ 能力。

---

# 第 21 章：让代码更快并调试

专注于如 `[[likely]]`、`[[unlikely]]` 和 `std::unreachable` 等属性。

---

## 食谱详情（示例）

### 食谱 1.1：字符串格式化

**问题：** 我们想要一种简单的方法格式化文本。

**解决方案：** C++20 引入了 `std::format`。

```cpp
#include <iostream>
#include <format>
#include <string>

int main() {
    std::string name = "World";
    std::cout << std::format("Hello, {}!\n", name);
    return 0;
}
```

### 食谱 5.1：可移动 (Movable)

**问题：** 我们需要一种机制来验证对象是否可以移动。

**解决方案：** C++20 拥有 `std::movable` 概念。

```cpp
#include <iostream>
#include <concepts>

struct MyClass {
    int value;
    MyClass(int v) : value(v) {}
    MyClass(MyClass&&) noexcept = default;
};

static_assert(std::movable<MyClass>);
```

### 食谱 10.1：什么是模块 (Module)

**问题：** 我们想要一种更好的组织代码的方法。

**解决方案：** C++20 引入了模块。

```cpp
// MyModule.cpp
export module MyModule;

export void SayHello() {
    std::cout << "Hello from module!" << std::endl;
}

// main.cpp
import MyModule;
#include <iostream>

int main() {
    SayHello();
    return 0;
}
```
