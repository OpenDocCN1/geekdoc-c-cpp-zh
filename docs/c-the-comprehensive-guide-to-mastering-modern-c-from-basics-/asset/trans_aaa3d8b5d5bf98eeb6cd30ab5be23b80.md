

接口？`area` 方法接收的不是一组 `Rectangle` 或 `Circle`，而是 `Shape`。

接口的特征在于它不提供实现，而只描述函数声明。这正是 `Shape` 通过将所有方法声明为纯虚函数（即 `virtual` 且 `= 0`）所完成的。在其他语言中，这被称为抽象方法。一个至少有一个抽象方法的类被称为抽象类。完全由抽象方法的类称为签名类（signature classes）。这个术语在其他语言中较为人知。在 Java 中，这类类被称为接口。（Java 接口也可以包含带有默认方法的实现实现，但我在这里将忽略这一点。）

# 动态多态

`area()` 方法不能将 `Shape` 作为值参数，因为否则参数将根据 `Shape` 的规则进行拷贝——即如列表 19.1 所示，发生切片（sliced）。出于相同的原因，`vector<Shape>` 也是不允许的，因为其中只会存储切片副本。而且由于 `Shape` 是一个抽象类（带有为 0 的虚函数的类），编译器也会报错。

因此，`vector` 存储指向 `Shape` 实例的指针。为了自动完成清理，我立即使用了 `unique_ptr`，但这是偶然的。`unique_ptr` 现在允许动态多态：每个指针都知道它指向 `Rectangle` 还是 `Circle`。当我调用 `area()` 时，正确的方法会被动态调用——但是因为该方法被标记为 `virtual`。你可以在第 15 章阅读它是如何工作的。

在示例中，`Rectangle` 和 `Circle` 分别派自 `Shape`。如果这些类中的某些具有其他接口怎么办？你可以通过多继承简单地添加；参见第 18 章。我建议在 C++ 中参考 Java，仅对签名类使用多重继承；最多一个祖先应该是非签名类。我在这里重复这一点，是因为我觉得非常重要。

# OCP 和 SRP 紧密相关

很多时候，违反 SRP 同时也意味着违反了 OCP，反之亦然。一个只需要局部更改的代码可能只会导致模块的替换。一个通过接口清晰划分的系统也可能按照职责进行清晰划分。

# 里斯科夫替换原则 (Liskov Substitution Principle)

对于像大众和汽车之类的车辆，听起来清晰且逻辑，但在实践中是一个障碍。这不仅关乎类型关系，还关乎它们的行为。覆盖方法允许抛出不同的异常吗？对参数和返回值有什么限制？`final` 方法如果调用任何非 `final` 方法会违反 LSP 吗？在复杂的层次结构中，通常需要询问是否违反了 LSP。这并不简单，常识会有帮助。

一个示例，甚至是经典的 LSP 违反示例，是围绕着 `rectangle` 和 `square` 的几何形状。直觉上，人们可能会构建一个 `Rectangle` 是基类、`Square` 是派生类的层次结构，square 是 rectangle，对吗？

```
// https://ggdbolt.org/z/rc67Wf
#include <iostream>
struct Point { int x, y; };
class Rectangle {
protected:
    Point origin;
    int width;
    int height;
public:
    Rectangle(Point o, int w, int h) : origin{o}, width{w}, height{h} {}
    virtual void setHeight(int height) { height = height; }
    virtual int getHeight() const { return height; }
    virtual void setWidth(int width) { width = width; }
    virtual int getWidth() const { return width; }
    virtual int getArea() const { return width * height; }
};
class Square : public Rectangle {
public:
    Square(Point o, int wh, int wh) : Rectangle(o, wh, wh) {}
    void setHeight(int height) override { height = height; }
    virtual setWidth(int width) override { width = width; }
};
void areaCheck(Rectangle& rect) {
    rect.setWidth(5);
    rect.setHeight(4);
    auto areaValue = rect.getArea();
    if(areaValue != 20) {
        std::cout << "error!\n";
    } else {
        std::cout << "all fine\n";
    }
}
int main() {
    Rectangle rect{{0,0}, 0, 0};
    areaCheck(rect); // 输出: all fine
    Square square{{0,0}, 0, 0};
    areaCheck(square); // 输出: error!
}
```

# 列表 19.6 返回类型的协变。

