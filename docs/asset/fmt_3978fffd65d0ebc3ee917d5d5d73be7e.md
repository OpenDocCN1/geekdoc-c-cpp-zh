
`dynamic_cast<Dog&>(myConfusedAnimal).eat();` // 调用 `Dog::eat()`

`myConfusedAnimal.Dog::eat();` // 调用 `Dog::eat()`

派生类本身的方法也可以通过使用访问成员的相同语法——`::` 运算符来显式消除同名方法的歧义。例如，`DogBird` 类可以通过定义自己的 `eat()` 方法来防止其他代码中的歧义错误。在该方法内部，它可以决定调用哪个父类版本。

```cpp
void DogBird::eat ()
{
    Dog::eat(); // 显式调用 Dog 版本的 eat ()
}
```

另一种防止歧义错误的方法是使用 `using` 语句明确说明在 `DogBird` 中应该继承哪个版本的 `eat`。这在下面的 `DogBird` 定义中实现：

```cpp
class DogBird : public Dog, public Bird
{
public:
    using Dog::eat; // 显式继承 Dog 版本的 eat()
};
```

另一种引发歧义的方法是多次继承同一个类。例如，如果 `Bird` 类由于某种原因继承了 `Dog`，那么 `DogBird` 的代码将无法编译，因为 `Dog` 变成了一个歧义基类。

```cpp
class Dog {};
class Bird : public Dog {};
class DogBird : public Dog, public Bird {}; // 错误！Dog 是歧义基
```

大多数歧义基类的情况要么是人为构造的假设示例（如上述），要么源于复杂的类层次结构。图 9-8 显示了上述示例的类图，指示了歧义。

歧义也发生在数据成员上。如果 `Dog` 和 `Bird` 都具有相同名称的数据成员，当客户端选择访问该成员时就会发生歧义错误。

## 歧义基类

更有可能的情况是多个父类本身具有共同的父类。例如，`Bird` 和 `Dog` 都继承自 `Animal` 类，如图 9-9 所示。

这种类层次结构在 C++ 中是允许的，但仍可能发生命名歧义。例如，如果 `Animal` 类有一个名为 `sleep()` 的公共方法，那么在 `DogBird` 对象上无法调用该方法，因为编译器不知道调用 `Dog` 继承的版本还是 `Bird` 继承的版本。

使用这些“菱形”类层次结构的最佳方法是将顶层类变为抽象基类，并将所有方法声明为 `virtual`。由于该类只声明方法而不提供定义，基类中没有方法可以调用，因此在该层级没有歧义。

![](img/a5a77830a2588caaa564a7658d3af652_294_0.png)

以下示例实现了一个菱形类层次结构，其中包含纯虚拟 `eat()` 方法由每个派生类定义。`Dog` 类仍然需要明确它使用哪个父类的 `eat()`，但任何歧义都是由 `Dog` 和 `Bird` 拥有相同方法引起的，而不是因为它们继承自同一个类。

```cpp
class Animal {
public:
    virtual void eat() = 0;
}
class Dog : public Animal {
public:
    virtual void bark() { cout << "Woof!" << endl; }
    virtual void eat() override { cout << "The dog has eaten." << endl; }
}
class Bird : public Animal {
public:
    virtual void chirp() { cout << "Chirp!" << endl; }
    virtual void eat() override { cout << "The bird has eaten." << endl; }
}
class DogBird : public Dog, public Bird {
public:
    using Dog::eat;
};
```

## 有趣且晦涩的继承问题

扩展类会带来各种问题。类的哪些特征是不能改变的？神秘的 `virtual` 关键字究竟是做什么的？这些问题以及更多问题将在后续章节中得到解答。

# 修改被重写方法的特征

在大多数情况下，重写一个方法是为了改变它的实现。有时，你可能想要改变该方法的其他特征。

## 修改方法的返回类型

一个经验是，重写方法时使用与基类使用的完全相同的方法声明（或方法原型）。实现可以改变，但原型保持不变。

然而，情况并非如此。在 C++ 中，重写的方法可以更改返回类型，只要原始返回类型是指针或引用，且新的返回类型指向派生类的指针或引用。此类类型被称为协变返回类型。当基类和派生类处理并行层次结构中的对象时，这一特性将非常有用。也就是说，另一组类与第一个类层次结构是切相关但相关的。

例如，考虑一个假设的樱桃园模拟器。你可能有两个类层次结构，它们模拟现实世界对象但显然相关。第一个是樱桃链（Cherry chain）。基类 `Cherry` 有一个名为 `BingCherry` 的派生类。同样，还有另一个类链，其基类为 `CherryTree`，派生类为 `BingCherryTree`。图 9-10 显示这两个类。

| Cherry | CherryTree |
|---|---|
| BingCherry | BingCherryTree |

图 9-10

现在假设 `CherryTree` 类有一个虚方法 `pick()`，它可以从树上获取单颗樱桃：

```cpp
Cherry CherryTree::pick()
{
    return new Cherry();
}
```

在 `CherryTree` 派生类中，你可能想要重写这个方法。也许 Bing樱桃在采摘时需要抛光（请听我说）。因为 `BingCherry` 是一个 `Cherry`，你可以保持方法原型不变，并如例所示重写该方法。`BingCherry` 指针会自动转换为 `Cherry` 指针。注意，此实现使用了 `unique_ptr` 以确保在 `polish()` 抛出异常时不会内存泄漏。

```cpp
Cherry BingTree::pick()
{
    auto theCherry = std::make_unique<BingCherry>();
    theCherry->polish();
    return theCherry.release();
}
```

上面的实现是完全没，可能我也会那样写。然而，由于你知道 `BingCherry` 将始终返回 `BingCherry` 对象，你可以通过更改返回类型来向该类的潜在用户指示这一点，如下：

```cpp
BingCherry* BingCherry::pick()
{
    auto theCherry = std::make_unique<BingCherry>();
    theCherry->polish();
    return theCherry.release();
}
```

判断是否可以更改重写方法的返回类型的好方法是考虑现有代码是否仍然有效，即里基夫替换原则（LSP）。在在上述示例中，更改返回类型是可以的，因为你假设 `pick()` 方法始终返回一个 `Cherry*`，这仍然可以编译并正常运行。因为 `BingCherry` 是一个 `Cherry`，任何在 `CherryTree` 版本的 `pick()` 结果上调用的方法，都仍然可以在 `BingTree` 版本的 `pick()` 结果上调用。

例如，你不能将返回类型更改为完全无关的内容，例如 `void*`。以下代码将无法编译：

```cpp
void* BingTree::pick() // Error
    auto theCherry = std::make_unique<BingCherry>();
    theCherry->polish();
    return theCherry.release();
}
```

这将生成一个编译器错误，类似于“'BingTree::pick': overriding virtual return type differs and is not covariant from 'CherryTree'”。

## 修改方法的参数

如果你在派生类的定义中使用父类中某个虚方法的名称，但使用的参数与父类中的方法不同，那么它并不是在重写父类的方法——它是在创建一个新方法。回到本章早些之前的 `Super` 和 `Sub` 示例，你可以尝试用新参数在 `Sub` 中重写 `someMethod()`：

```cpp
class Super
{
    public:
    Super();
    virtual void someMethod();
};

## 有趣且晦涩的继承问题

class Sub : public Super {
    public:
    Sub();
    virtual void someMethod(int i); // 可以编译，但没有重写
    virtual void someMethod();
}
```

该方法的实现可能如下：

```cpp
void Sub::someMethod(int i) {
    cout << "This is Sub's version of someMethod with " << i << endl;
}
```

上述类定义可以通过编译，你并没有重写 `someMethod()`。因为参数不同，你创建了一个接受 `int` 的新方法 `someMethod()`，而你希望它只对 `Sub` 对象有效，因此前面的代码是正确的。事实上，C++ 标准规定，对于 `Sub` 而言，原始方法现在被隐藏了。下面的示例代码无法编译，因为不再有无参数的 `someMethod()` 版本。

```cpp
Sub Sub;
Sub.someMethod(); // Error! hidden.
```

如果你确实打算重写基类中的 `someMethod()`，那么你应该为 `Sub` 的 `someMethod(int)` 声明标记 `override` 标识符。这样做，编译器将给出一个错误，说明 `someMethod(int)` 没有重写基类中的方法。

有一种相当晦涩的技术可以让你“鱼和掌兼得”。也就是说，你可以使用这种技术在派生类中用新原型有效地“重写”方法，但又继续继承基类的定义。这种技术使用 `using` 关键字将基类的方法定义包含在派生类中，如下所示：

```cpp
class Super {
    public:
    Super();
    virtual void someMethod();
}
class Sub : public Super {
    public:
    Sub();
    using Super::someMethod; // 显式继承 Super 版本
    virtual void someMethod(int i); // 添加一个新版本的 someMethod
    virtual void someMethod();
}
```

## override 关键字

注意：在派生类中找到一个与基类方法同名但使用不同参数列表的方法是非常罕见的。

有时，可能会不小心创建一个新方法，而不是重写基类的方法。考虑接下来的 `Super` 和 `Sub` 类，其中 `Super` 正确地重写了 `someMethod()`：

```cpp
class Super
  public:
    Super();
    virtual void someMethod(double d);
class Sub : public Super
  public:
    Sub();
    virtual void someMethod(double d);
```

你可以通过引用调用 `someMethod()`，如下：

```cpp
Sub mySub;
Super& ref = mySub;
ref.someMethod(1.1);
```

这会调用 `Sub` 类的 `someMethod()`。现在，假设你在重写 `someMethod()` 时使用了整数参数而不是 `double`：

```cpp
class Sub : public Super
  public:
    Sub();
    virtual void someMethod(int i);
```

如在前一节所示，这段代码不会重写 `someMethod()`，而是创建一个新的虚方法。如果你通过引用尝试调用 `someMethod()`，如下：

```cpp
Sub mySub;
Super& ref = mySub;
ref.someMethod(1.1); // 调用 Super 版本的 someMethod()
```

这种类型的问题发生在你想要修改基类但忘记更新所有派生类时。例如，可能你的 `Super` 类的初始版本有一个接受 `int` 的 `someMethod()`。你后来决定编写 `Sub` 类并重写这个接受 `int` 的 `someMethod()`。Sub 需要 `double` 而不是 `int`，所以你更新了基类中的 `someMethod()`。可能会在某个时候，你忘记更新派生类中的 `someMethod()` 方法以接受 `double` 而不是 `int`。由于忘记这样做，你现在实际上是在创建一个虚方法，而不是正确地重写它。

你可以通过如下使用 `override` 关键字来防止这种情况：

```cpp
class Sub : public Super
  public:
    Sub();
    virtual void someMethod(int i) override;
};
```

`Sub` 的定义将生成编译器错误，因为你表示 `someMethod()` 应该重写基类中的方法，但在 `Super` 类中没有接受 `int` 的 `someMethod()`，只有一个接受 `double` 的。

意外创建新方法而不是正确重写方法的问题也会发生在你重命名基类中的方法，但忘记重命名派生类中的重写方法时。

在本章示例中已经使用了 `override` 关键字，建议在想要重写基类方法时使用它。

## 继承的构造函数

在前面的节中，你看到了使用 `using` 关键字将基类定义显式包含在派生类中。这对于普通类方法非常有效，但也适用于构造函数，允许你从基类继承构造函数。查看以下 `Super` 和 `Sub` 类的定义：

```cpp
class Super
  public:
    Super(const std::string& str);
class Sub : public Super
  public:
    Sub(int i);
```

你只能通过提供的 `Super` 构造函数构造 `Super` 对象，它需要一个字符串作为参数。相反，构造 `Sub` 对象只能通过提供的 `Sub` 构造函数进行。

构造函数，需要单个整数作为参数。你不能使用 Super 类中定义的接受字符串的构造函数来构造 Sub 对象。例如：

```
Super super("*Hello"); // OK，调用基于字符串的 Super 构造函数
Sub sub1(1);      // OK，调用基于整数的 Sub 构造函数
Sub sub2("*Hello"); // Error，Sub 没有继承字符串的 Sub 构造函数
```

如果你希望能够基于字符串的 Super 构造函数来构造 Sub 对象，可以在 Sub 类中显式继承 Super 构造函数，如下所示：

```
class Sub : public Super
{
public:
    using Super::Super;
    Sub(int i);
};
```

现在你可以通过以下方式构造 Sub 对象：

```
Sub sub1(1);      // OK，调用基于整数的 Sub 构造函数
Sub sub2("*Hello"); // OK，调用继承的基于字符串的 Super 构造函数
```

Sub 类可以定义一个参数列表与 Super 类中某个构造函数相同的构造函数。在这种情况下，与任何重写一样，Sub 类的构造函数优先于继承的构造函数。在这个示例中，Sub 类使用关键字继承了 Super 类所有的构造函数。然而，由于 Sub 类定义了自己的带有类型为 float 的单参数构造函数，继承自 Super 类的带有类型为 float 的单参数构造函数被重写了。

```cpp
class Super
{
public:
    Super(const std::string& str);
    Super(float f);
};
class Sub : public Super
{
public:
    using Super::Super;
    Sub(float f); // 重写了继承的基于 float 的 Super 构造函数
};
```

有了此定义，可以如下创建 Sub 对象：

```
Sub sub("*Hello"); // OK，调用继承的基于字符串的 Super 构造函数
Sub sub2(1.23f);    // OK，调用基于 float 的 Sub 构造函数
```

使用 using 子句从基类继承构造函数时存在一些限制。当你从基类继承一个构造函数时，你会继承所有的构造函数。无法只继承基类构造函数的子集。第二个限制与多重继承有关。如果另一个基类有一个具有相同参数列表的构造函数，则无法从其中一个基类中继承构造函数，因为这会导致歧义。为了解决这个问题，Sub 类需要显式定义冲突的构造函数。例如，下面的 Sub 类尝试从 Super1 和 Super2 两个基类继承所有的构造函数，这由于基于 float 的构造函数的歧义导致了编译错误。
