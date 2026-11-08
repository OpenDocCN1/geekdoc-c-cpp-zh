
```cpp
int main()
{
    Line l;
    Circle c1, c2;

    myDraw(l);          // myDraw(Line)(GeoObj&) => Line
    myDraw(c1);         // myDraw(Circle)(GeoObj&) => Circle

    distance(c1, c2);   // distance=Circle, Circle(GeoObj&)
    distance(c1, c1);   // distance=Circle, Circle(GeoObj&)

    // std::vector<GeoObj*> coll; // ERROR: no heterogeneous collection
    std::vector<Circle> coll;     // OK: homogeneous collection
    coll.push_back(c1);           // insert Circle
    drawElements(coll);           // draw all circles
}
```

与 `myDraw()` 一样，`draw()` 不能再作为 `distance()` 的具体参数类型使用。取而代之，我们提供两个函数模板 `GeoObj1` 和 `GeoObj2`，它们使接口能够接受几何对象的不同组合。

[点击此处查看代码图像](#)

```cpp
distance(c1, c2);    // distance=Circle, Circle?
                     // (GeoObj1&, GeoObj2&)
```

然而，异构集合再也无法被透明地处理。这正是静态多态中的“静态”部分施加约束之处：所有类型都必须在编译期确定。不过，我们可以轻松地为不同的几何对象类型引入不同的集合。集合不再需要仅限于指针，这在性能和类型安全方面可能具有显著优势。

## 18.3 动态多态与静态多态

让我们对这两种多态形式进行分类和比较。

### 术语

动态多态和静态多态为不同的 C++ 编程惯用法提供支持：

- **通过继承实现的多态是有界且动态的：**
  - **有界**意味着参与多态行为的类型的接口由公共基类的设计预先确定（该概念的其他术语是接口或抽象基类）。
  - **动态**意味着接口的绑定在运行时（动态地）完成。
- **通过模板实现的多态是无界且静态的：**
  - **无界**意味着参与多态行为的类型的接口不是预先确定的（该概念的其他术语是非侵入式和非侵入性）。
  - **静态**意味着接口的绑定在编译期（静态地）完成。

因此，严格来说，在 C++ 术语中，动态多态和静态多态是有界动态多态和无界静态多态的简称。换句话说，这里使用的是动态多态（即 Smalltalk 提供的是无界动态多态）。然而，在 C++ 的语境中，更简洁的术语“动态多态”和“静态多态”不会引起混淆。

### 优点与缺点

C++ 中的动态多态具有以下优点：

- 异构集合可以得到优雅处理。
- 可执行代码大小可能更小（因为只需要一个多态函数，而针对不同类型必须生成不同的模板实例）。
- 代码可以完全复制；因此不必分发实现源代码（包含模板库时通常需要分发模板实现的源代码）。
- 只提供部分接口的具体类型仍然可以使用，只要应用程序最终只用到那部分接口。

静态多态通常被认为比动态多态更具类型安全性。使用指向公共基类的指针时，这些指针有可能无意中最终指向不同类型的完整对象。

在实践中，当不同的语义假设隐藏在看起来相同的接口背后时，模板实例化也可能带来一些麻烦。例如，当一个假定运算符 + 满足结合律的模板被实例化用于一个在该运算符上不满足结合律的类型时，就可能出现意外。在实践中，这种语义不匹配比其他基于接口的启发式方法更少发生，主要因为接口规范被更明确地规定。

### 结合两种形式

当然，你可以结合两种多态形式。例如，你可以从公共基类派生出不同种类的几何对象，以便处理几何对象的异构集合。不过，你仍然可以使用模板为某一类几何对象编写代码。

继承与模板的结合将在第 21 章进一步描述。我们将（除其他内容外）看到如何参数化成员函数的虚特性，以及如何使用基于继承的奇异递归模板模式（CRTP）为静态多态提供额外的灵活性。

## 18.4 使用概念

反对使用模板实现静态多态的一个论点是，接口的绑定通过实例化相应模板来完成。这意味着没有可供编程所针对的公共接口（例如基类）。相反，只要所有实例化代码都有效，模板的任何使用都能正常工作。如果无效，则可能导致难以理解的错误消息，甚至使原本有效的代码突然失效。

为此，C++ 语言设计者一直在研究显式提供（并检查）模板参数接口的能力。这样的接口在 C++ 中通常称为概念（concept）。它表示模板实参为了成功实例化模板而必须满足的一组约束。

尽管在这一领域已有多年的工作，但截至 C++17，概念仍然不是标准 C++ 的一部分。一些编译器为此类特性提供实验性支持。不过，概念很可能成为 C++17 之后的下一个标准的一部分。

概念可以理解为静态多态的一种“接口”。在我们的示例中，它可能如下所示：

**点击此处查看代码图像**

poly/conceptreq.cpp

```cpp
#include "coord.hpp"

template<typename T>
concept GeoObj = requires(T x) {
  { x.draw() } -> void;
  { x.center_of_gravity() } -> Coord;
  ...
};
```

这里，我们使用关键字 concept 定义概念 GeoObj，它约束一个类型具有可调用的成员 draw() 和 center_of_gravity()，并具有适当的返回类型。

现在，我们可以重写一些示例模板，以包含一个 requires 子句，用 GeoObj 概念约束模板参数：

**点击此处查看代码图像**

poly/conceptzoo.cpp

```cpp
template<typename T>
requires GeoObj<T>
void draw (T const& obj)
{
  obj.draw();
}
```

poly/conceptzoo.hpp

```cpp
#include "concept.hpp"

#include <vector>

// draw any GeoObj

template<typename T>
requires GeoObj<T>
void myDraw (T const& obj)
{
  obj.draw();   // call draw() according to type of obj
}

template<typename T1, typename T2>
requires GeoObj<T1> && GeoObj<T2>
Coord distance(T1 const& x1, T2 const& x2)
{
    Coord c = x1.center_of_gravity() - x2.center_of_gravity();
    return c.norm();  // return coordinates as absolute
}

// draw homogeneous collection of GeoObjs
template<typename T>
requires GeoObj<T>
void drawAll(std::vector<T> const& elems)
{
    for (std::size_t i=0; i<elems.size(); ++i) {
        elems[i].draw();  // call draw() according to ...
    }
}
```

对于能够参与（静态）多态行为的类型，这种方法仍然是非侵入式的：

**点击此处查看代码图像**

```cpp
// concrete geometric object class Circle
// not derived from any class or implementing any interface
class Circle {
public:
    void draw() const;
    Coord center_of_gravity() const;
};
```

也就是说，此类类型仍然是在没有任何特定基类或 requires 子句的情况下定义的，并且仍然可以是基础数据类型或来自独立框架的类型。

附录 L 包含对 C++11 概念的更详细讨论；人们期待它们进入新的 C++ 标准。

## 18.5 设计模式的新形式

传统上，C++ 中的静态多态会带来实现经典设计模式的新方式。以桥接模式为例，它在许多 C++ 程序中扮演重要角色。使用桥接模式的一个目标是在接口的不同实现之间切换。

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_259_0.png)

*图 18.3. 使用继承实现的桥接模式*

根据 [DesignPatternsGoF]，这通常通过一个接口类完成，该接口类暴露指向实现的指针，并通过该指针委托所有调用（见图 18.3）。然而，如果实现的类型在编译期已知，我们反而可以利用模板的能力（见图 18.4）。这会带来更高的类型安全性（部分原因是避免了指针转换）和更好的性能。

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_259_1.png)

*图 18.4. 使用模板实现的桥接模式*

## 18.6 泛型编程

静态多态引出了泛型编程的概念。然而，泛型编程并没有一个公认的唯一定义（正如面向对象编程也没有一个公认的唯一定义）。根据 [Czarnecki et al.]，泛型编程是计算机科学的一个分支学科，研究如何发现和利用高效算法、数据结构及其他软件组件的共性，并对其进行系统化组织。
