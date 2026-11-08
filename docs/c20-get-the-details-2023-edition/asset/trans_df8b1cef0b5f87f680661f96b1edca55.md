
```cpp
void implicitCall1() & {
    std::cout << "non const lvalue";
}

void implicitCall1() const& {
    std::cout << "const lvalue";
}

void implicitCall1() && {
    std::cout << "non const rvalue";
}

void implicitCall1() const&& {
    std::cout << "const rvalue";
}

};

int main() {
    std::cout << '\n';

    Test test;
    const Test constTest;

    test.explicitCall1("test");
    constTest.explicitCall1("constTest");
    std::move(test).explicitCall1("std::move(test)");
    std::move(constTest).explicitCall1("std::move(constTest)");

    std::cout << '\n';
}
```

第13、17、21和25行是所需的函数重载。第13行和第17行接受非const和const左值对象；第21行和第25行接受非const和const右值对象。第7行中的推导this使其能够在一个成员函数中去重这四个重载，并完美转发 `self`（第9行）并调用 `implicitCall1`。

```cpp
    std::string name;
};

class Body {};

class Engine {};

class Car;

using CarElement = std::variant<Wheel, Body, Engine, Car>;

class Car {
public:
    Car(std::initializer_list<CarElement*> carElements) :
        elements(carElements) {}

    template<typename T>
    void visitCarElements(T&& visitor) const {
        for (auto elem : elements) {
            std::visit(visitor, *elem);
        }
    }

private:
    std::vector<CarElement*> elements;
};

overloaded carElementPrintVisitor {
    [](const Body& body)      { std::cout << "Visiting body" << '\n'; },
    [](this auto const& self, const Car& car) {
        car.visitCarElements(carElementPrintVisitor(self));
        std::cout << "Visiting car" << '\n';
    },
    [](const Wheel& wheel)    { std::cout << "Visiting "
                              << wheel.getName() << " wheel" << '\n'; },
    [](const Engine& engine)  { std::cout << "Visiting engine" << '\n'; }
};

overloaded carElementDoVisitor {
    [](const Body& body)      { std::cout << "Moving my body" << '\n'; },
    [](this auto const& self, const Car& car) {
        car.visitCarElements(carElementDoVisitor(self));
        std::cout << "Starting my car" << '\n';
    },
    [](const Wheel& wheel)    { std::cout << "Kicking my "
                              << wheel.getName() << " wheel" << '\n'; },
    [](const Engine& engine)  { std::cout << "Starting my engine" << '\n'; }
};
```

```cpp
64  int main() {
65
66      std::cout << '\n';
67
68      CarElement wheelFrontLeft  = Wheel("front left");
69      CarElement wheelFrontRight = Wheel("front right");
70      CarElement wheelBackLeft   = Wheel("back left");
71      CarElement wheelBackRight  = Wheel("back right");
72      CarElement body            = Body();
73      CarElement engine          = Engine();
74
75      CarElement car = {&wheelFrontLeft, &wheelFrontRight,
76                        &wheelBackLeft, &wheelBackRight,
77                        &body, &engine};
78
79      std::visit(carElementPrintVisitor, engine);
80      std::visit(carElementPrintVisitor, car);
81      std::cout << '\n';
82
83      std::visit(carElementDoVisitor, engine);
84      std::visit(carElementDoVisitor, car);
85      std::cout << '\n';
86
87  }
```

car（第75行）代表对象层次结构，两个操作访问它，即 `carElementPrintVisitor`（第45行）和 `carElementDoVisitor`（第54行）。推导this使得第47行和第58行中访问汽车的lambda表达式能够引用隐式lambda对象来访问汽车的组件：`car.visitCarElements(self)`。

![](img/c60a87adb7f61e2e82071d081bbb389a_610_0.png)

## 重载模式

### 8.1.1.1.3 简化CRTP

但CRTP是什么意思？CRTP是C++惯用法“奇异递归模板模式”（Curiously Recurring Template Pattern）的缩写，指的是C++中的一种技术：类 `Derived` 从类模板 `Base` 派生。关键在于 `Base` 将 `Derived` 作为模板参数。

```cpp
template <typename T>
class Base{
    ...
};

class Derived : public Base<Derived>{
    ...
};
```

CRTP通常用于在编译时实现多态。更多信息，请阅读我的文章[关于动态和静态多态的更多内容](https://www.modernescpp.com/index.php/more-about-dynamic-and-static-polymorphism)。

得益于显式对象参数，我可以从CRTP缩略词中去掉C和R。

#### 简化CRTP

```cpp
// deducingThisCRTP.cpp

#include <iostream>

struct Base{
    template <typename Self>
    void interface(this Self&& self){
        std::forward<Self>(self).implementation();
    }
    void implementation(){
        std::cout << "Implementation Base\n";
    }
};

struct Derived1 : Base {
    void implementation(){
        std::cout << "Implementation Derived1\n";
    }
};

struct Derived2 : Base {
    void implementation(){
    23    std::cout << "Implementation Derived2\n";
    24  }
    25 };

    27 struct Derived3 : Base {};

    29 template <typename T>
    30 void execute(T& base){
    31     base.interface();
    32 }


    35 int main(){

    37     std::cout << '\n';

    39     Derived1 d1;
    40     execute(d1);

    42     Derived2 d2;
    43     execute(d2);

    45     Derived3 d3;
    46     execute(d3);

    48     std::cout << '\n';

    50 }
```

显式对象参数允许推导出派生类型并完美转发它（第7行）。使用了第32行中的具体类型——`Derived1`（第39行）、`Derived2`（第42行）和`Derived3`（第45行）。因此，会调用相应的虚函数实现：`std::forward<Self>(self).implementation();`

![](img/c60a87adb7f61e2e82071d081bbb389a_613_0.png)

简化CRTP

## 8.1.2 标准库

### 8.1.2.1 范围扩展

在C++23中，ranges库获得了强大的扩展。这一扩展包括一种构造容器的便捷方式、各种新视图，以及随 `std::generator` 出现的第一个具体协程。

#### 8.1.2.1.1 ranges::to

`std::ranges::to` 是一种从范围构造容器的便捷方式：

```cpp
std::vector<int> range(int begin, int end, int stepsize = 1) {
    auto boundary = [end](int i){ return i < end; };
    std::vector<int> result = std::ranges::views::iota(begin)
                            | std::views::stride(stepsize)
                            | std::views::take_while(boundary)
                            | std::ranges::to<std::vector>();
    return result;
}
```

函数 `range` 创建一个 `std::vector<int>`，其中包含从 `begin` 到 `end` 的所有元素，步长为 `stepsize`。`begin` 必须小于 `end`。得益于 `std::ranges::to`，这些元素可以直接推入 `std::vector`。

#### 8.1.2.1.2 新视图

C++23 支持额外的视图：

#### C++23 中的视图

| 视图 | 描述 |
|---|---|
| `std::ranges::zip_view`<br>`std::views::zip` | 创建元组视图。 |
| `std::ranges::zip_transform_view`<br>`std::views::zip_transform` | 通过应用转换函数创建元组视图。 |
| `std::ranges::adjacent_view`<br>`std::views::adjacent` | 创建相邻元素的视图。 |
| `std::ranges::adjacent_transform_view`<br>`std::views::adjacent_transform` | 通过应用转换函数创建相邻元素的视图。 |
| `std::ranges::join_with_view`<br>`std::views::join_with` | 通过应用分隔符将现有范围连接成视图。 |
| `std::ranges::slide_view`<br>`std::views::slide` | 通过接受一个视图和数字 N 创建 N 元组。 |
| `std::ranges::chunk_view`<br>`std::views::chunk` | 通过接受一个视图和数字 N 创建 N 块。 |
| `std::ranges::chunk_by_view`<br>`std::views::chunk_by` | 基于谓词创建视图的块。 |
| `std::ranges::as_const_view`<br>`std::views::as_const` | 将视图转换为常量范围。 |
| `std::ranges::as_rvalue_view`<br>`std::views::as_rvalue` | 将每个元素转换为右值。 |
| `std::ranges::stride_view`<br>`std::views::stride` | 创建另一个视图的第 N 个元素的视图。 |

以下代码片段应用了新视图。

