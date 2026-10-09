

`class Rectangle;`

这是对编译器的承诺，表明我们最终会声明这些类。随后，编译器将允许将它们用作参数和返回类型。但是，在类被完整声明之前，无法将其用作成员变量或超类。

这就引出了一个问题：在 `C++` 文件中，按照什么正确的顺序来放置所有的声明、定义等。以下是我的建议。你应该按照以下顺序编写 `cpp` 文件。

1.  包含语句（Include statements）。
2.  `using namespace` 语句。
3.  类的前向声明。
4.  类声明和函数声明。
5.  函数定义和成员定义。
6.  测试（其他项目可能有不同的测试惯例）。

## 12.8 static 关键字

有时你可能希望将一个函数与类关联，但不与特定的实例关联。以下是你这样做的一些原因。

-   该函数旨在构造实例——所谓的*工厂方法*。我们将在下一章中看到一个详细的示例。
-   该函数操作于实例的向量，因此你无法合理地将其与特定实例关联。
-   该函数旨在一次性改变所有实例的行为。例如，你可能希望为一个类启用额外的日志信息以帮助调试。
-   该函数旨在管理你类的所有实例。例如，由于第一次连接数据库很慢，你可能希望维护一个包含到给定数据库的十个连接的池。然后你可以将函数与 `DatabaseConnection` 类关联，允许你从这个池中获取和返回连接。

如果你希望将一个函数与类关联，而不是与任何实例关联，你应该使用关键字 `static`。你还可以声明一个成员变量是 `static`，这意味着它被该类的所有实例共享。

作为一个略显牵强的例子，假设我们发现了代码中的一个性能问题。我们怀疑它与 `sin` 函数相关，这是我们在一个计算 `sin` 函数的类中编写的 `evaluate` 函数的一部分。作为调试的一部分，我们想要计算该方法被调用的确切次数。以下是我们可以做到的一点方法：

```c++
class CallCountedSin : public RealFunction {
public:
    static int getNumberOfCalls();
    double evaluate(double x) {
        numCalls++;
        return sin(x);
    }
private:
    static int numCalls;
};
```

我们的类 `CallCountedSin` 表现得像 `sin` 函数，但还统计在 `any` 实例上调用 `evaluate` 的次数。我们有一个 `static` 成员变量来保存调用次数，以及一个 `static` 成员函数来读取该值。

函数的定义看起来就像普通的成员函数一样。

```c++
int CallCountedSin::getNumberOfCalls() {
    return numCalls;
}
```

请注意，此函数不允许访问除 `static` 变量以外的任何变量。

以下是如何初始化静态变量 `numCalls`：

```c++
int CallCountedSin::numCalls = 0;
```

这看起来很像全局变量定义。在某种意义上，它确实就是。区别在于我们将变量 `numCalls` 与类 `CallCountedSin` 关联了起来。这比拥有一个名为 `numCalls` 的全局变量要好，因为静态变量可以声明为私有。这意味着它不可能被其他类中的任何函数使用。

以下是如何实际调用静态函数的示例：

```c++
void testCallCountedSin() {
    CallCountedSin instance1;
    CallCountedSin instance2;
    integral(instance1, 0, 1, 1000);
    integral(instance2, 0, 1, 1000);
    int numCalls=CallCountedSin::getNumberOfCalls();
    ASSERT(numCalls == 2000);
}
```

要注意的一点是，要调用该函数，我们必须用类名限定其名称。

```c++
int numCalls=CallCountedSin::getNumberOfCalls();
```

由于我们可能有多个类具有相同命名的静态方法，因此需要限定名称是有意义的。

我们在第 9.3 节中已经看到了一个静态变量的例子。你可能记得我们用以下代码重置了随机数发生器的种子：

```c++
mersenneTwister.seed(mt19937::default_seed);
```

这段代码正在访问定义在类 `mt19937` 中的静态变量 `default_seed`。由于 `default_seed` 对所有实例都是相同的，因此将其与类而不是任何实例关联是合乎逻辑的。对于比单个整数更复杂的数据对象，让所有实例共享的一个变量只保留一份副本可能会节省大量内存。

总之，静态函数和静态变量完全像全局函数和全局变量一样工作，除了以下几点。

-   它们可以被设为私有，并拥有对私有数据的特权访问权限。这增加了封装性。
-   它们与类相关联。调用静态函数需要用类名进行限定。这防止了名称冲突。

令人困惑的是，C++ 还使用 `static` 关键字用于未定义在任何类中的函数。在此上下文中，`static` 意味着“不能在当前文件之外使用”。不幸的是，C++ 使用相同的关键词服务于两个完全不同的目的。

## 危险！

与其他全局变量一样，如果你正在使用多线程代码，那么在使用非常量静态变量时必须小心使用锁。参见第 20 章。

## 12.9 protected 关键字

我们已经知道可以使用关键字 `public` 或 `private` 进行信息隐藏。`public` 意味着每个人都可以使用方法和变量。`private` 意味着没有人可以使用方法/变量，包括子类。

既然我们正在使用子类，值得提到的是你也可以使用关键字 **protected**。这意味着只有子类可以使用方法/变量。在实践中，我建议你暂时忽略 **protected**，因为它并不特别有用。

### 练习

1.  12.9.1. 编写 **DigitalCallOption** 和 **DigitalPutOption** 类。重构 **PutOption** 使其继承自 **PathIndependentOption**。
2.  12.9.2. 编写一个代表亚洲期权的 **AsianOption**。展示这个新类在期权 UML 图中的位置。
3.  12.9.3. 为以 **Shape** 为基类的类层次结构创建一个 UML 图。
4.  12.9.4. 我们不同的图表类之间有很多相同的代码。特别是它们都有一个标题和两个名为 **writeAsHTML** 的函数。设计一个基类并为每个图表扩展它。绘制 resulting 层次的 UML 图。使用 getter 和 setter 方法访问标题。
5.  12.9.5. 你能使用本章的技术来改进为练习 10.6.6 编写的 **Cipher** 类吗？
6.  12.9.6. 这个练习测试静态变量和函数的使用。
    1.  编写一个接口类 **RandomNumberGenerator**，它具有生成均匀分布随机数的函数。
    2.  编写一个使用 **mt19937** 类的 **RandomNumberGenerator** 实现。这种通过简单地调用另一个类来完成所有工作来实现接口的设计模式被称为*委托*。
    3.  在 **RandomNumberGenerator** 类上编写一个名为 **setDefault** 的静态函数，用于设置当前的默认 **RandomNumberGenerator** 实例。注意，你应该使用 **shared_ptr<RandomNumberGenerator>** 作为 **setDefault** 的参数。
    4.  在 **RandomNumberGenerator** 上编写一个静态函数 **randUniform**，允许用户生成均匀分布的随机数，而无需创建 **RandomNumberGenerator**。
    5.  在 **RandomNumberGenerator** 中添加一个非静态的 **setDefault** 函数，将当前使用的随机数发生器设置为默认的随机数发生器。你需要使用 **this** 关键字。
    6.  你认为这在哪些方面（如果有的话）改进了 **matlib** 中现有的函数？

