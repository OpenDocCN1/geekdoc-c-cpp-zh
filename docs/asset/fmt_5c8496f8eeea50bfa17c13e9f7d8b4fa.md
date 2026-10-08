
`class Super1`

{

  public:

    `Super1(float f)`;

}

`class Super2`

{

  public:

    `Super2(const std::string& str)`;

    `Super2(float f)`;

}

`class Sub : public Super1, public Super2`

{

  public:

    `using Super1::Super1`;

    `using Super2::Super2`;

    `Sub(char c)`;

};

```
Sub 中的第一个 using 子句继承了 Super1 的构造函数。这意味着 Sub 将获得以下构造函数：
Sub(float f); // 继承自 Super1
```

在 `Sub` 的第二个 `using` 子句中，你尝试从 `Super2` 继承所有构造函数。然而，这将产生编译器错误，因为这意味着 `Sub` 将获得第二个 `Sub(float f)` 构造函数。通过在 `Sub` 类中如下所示显式声明冲突的构造函数可以解决此问题：

```
class Sub : public Super1, public Super2
{
  public:
    using Super1::Super1;
    using Super2::Super2;
    Sub(char c);
    Sub(float f);
};
```

使用继承的构造函数时，确保所有成员变量都已正确初始化。例如，考虑以下 `Super` 和 `Sub` 类的新定义。此示例在所有情况下都没有妥善地初始化 `mint` 数据成员，这是一个严重的错误。

```
class Super
{
public:
    Super(const std::string& str) : mStr(str) {}
private:
    std::string mStr;
};

class Sub : public Super
{
public:
    using Super::Super;
    Sub(int i) : Super(**), mInt(i) {}
private:
    int mInt;
};
```

你可以如下创建 `Sub` 对象：

```
Sub s1(2);
```

这将调用 `Sub(int i)` 构造函数，该构造函数将初始化 `Sub` 类的 `mInt` 数据成员，并调用带有空字符串的 `Super` 构造函数来初始化 `mStr` 数据成员。

由于 `Super` 构造函数在 `Sub` 类中被继承，你也可以如下构造 `Sub` 对象：

```
Sub s2("Hello World");
```

这将调用 `Sub` 类中继承的 `Super` 构造函数。然而，这个继承的 `Super` 构造函数只初始化 `Super` 类的 `mStr` 成员变量，而不初始化 `Sub` 类的 `mInt` 成员变量，处于未初始化状态。这通常是不建议的。

解决方案是使用类内成员初始化将 `mInt` 初始化为0。以下代码使用类内成员初始化将 `mInt` 初始化为 0。`Sub(int i)` 构造函数仍然可以更改初始化并将 `mInt` 初始化为构造函数参数 `i`。

```
class Sub : public Super
{
public:
    using Super::Super;
    Sub(int i) : Super(**), mInt(i) {}
private:
    int mInt = 0;
};
```

## 方法重写的特殊情况

在重写方法时，有几种特殊情况需要注意。本节概述了可能会遇到的情况。

### 基类方法是静态的

在 C++ 中，你不能重写静态方法。原因是虚函数不是在运行时根据对象类型解析的，而是在编译时根据引用的静态类型解析的。如果你尝试在类中声明虚静态函数，编译器将发出错误。

```cpp
class Base {
public:
    static void func() {
        cout << "Base::func()" << endl;
    }
};

class Derived : public Base {
public:
    static void func() {
        cout << "Derived::func()" << endl;
    }
};

Derived d;
Base* b = &d;
b->func(); // 调用 Base::func()
```

上面的输出将是：

```
Base::func()
```
这是因为调用是由指针的类型决定的，而不是它指向的对象。静态函数不是类实例的一部分。注意，静态函数没有 `this` 指针且不能是虚函数。

### 基类方法被重载

当你通过指定名称和参数集重载方法时，编译器会隐式隐藏基类中的所有同名实例。这种想法是，如果你重写了某个名称，你可能想要重写该名称的所有方法，但遗忘记了，这应该被视为错误。如果你仔细考虑，这是合理的——为什么你只想改变某些版本的方法而不是其他的？考虑以下子类，它重写了一个方法但没有重写其相关的兄弟方法：

```
class Super {
  public:
    virtual void overload() { cout << "Super's overload()" << endl; }
    virtual void overload(int i) {
      cout << "Super's overload(int i)" << endl;
    }
}

class Sub : public Super {
  public:
    virtual void overload() override { cout << "Sub's overload()" << endl; }
  };
```

如果你尝试在 `Sub` 对象上调用这个接受 `int` 参数的方法版本，你的代码将无法编译，因为它没有被显式重写。
`mySub.overload(2); // Error! 没有匹配的 overload(int) 方法.`

从 `Sub` 对象访问此版本的方法是可能的。你只需要指向 `Super` 对象的指针或引用。

```cpp
Sub mySub;
Super* ptr = &mySub;
ptr->overload(7);
```

在 C++ 中，隐藏未实现的重载方法仅仅停留在表面。显式声明为子类型实例的对象将不会使该方法可用，但简单地强制转换为基类将会让该方法重新出现。

使用 `using` 关键字可以避免重载所有你真正想要更改的一个版本的麻烦。在下面的代码中，`Sub` 类的定义使用了 `Super` 的一个 `overload()` 版本，并显式地重写了其他版本：

```cpp
class Super {
public:
    virtual void overload() { cout << "Super's overload()" << endl; }
    virtual void overload(int i) {
        cout << "Super's overload(int i)" << endl;
    }
}

class Sub : public Super {
public:
    using Super::overload;
    virtual void overload(int i) override { cout << "Sub's overload()" << endl; }
}
```

`using` 子句存在风险。假设在 `Super` 中添加了第三个 `overload()` 方法，该方法本应在 `Sub` 中被重写。由于 `using` 子句的存在，这不会被检测为错误；`Sub` 类的设计者显式地表示：“我愿意接受父类对此方法的其他所有重写。”

> 为了避免晦涩的错误，你应该显式地或通过 `using` 关键字来重写重载方法的所有版本，但要记住 `using` 子句的风险。

### 基类方法是 private 或 protected 的

重写 `private` 或 `protected` 方法没有问题。请记住，方法的访问限定符决定了是否可以调用它。仅仅因为派生类不能调用其父类的私有方法并不意味着它不能重写它们。事实上，重写 `private` 或 `protected` 方法是 C++ 中的一种常见模式。它允许派生类定义在基类中引用的“独特性”。注意，对于 Java 和 C#，只有重写 `public` 和 `protected` 方法是重要的，`private` 方法则不然。

例如，以下类是汽车模拟器的一部分，它根据油耗和剩余燃料量估计汽车可以行驶的里程数：

```cpp
class MilesEstimator {
public:
    virtual int getMilesLeft() const {
        return getMilesPerGallon() * getGallonsLeft();
    }
    virtual void setGallonsLeft(int keyValue) { mGallonsLeft = keyValue;}
virtual int getGallonsLeft() const { return mGallonsLeft; }
private:
    int mGallonsLeft;
    virtual int getMilesPerGallon() const { return 20; }
};
```

`getMilesLeft()` 根据其两个方法的结果进行计算。下面的代码使用 `MilesEstimator` 计算使用 2 加仑汽油可以行驶多少里程：

```cpp
MilesEstimator myMilesEstimator;
myMilesEstimator.setGallonsLeft(2);
cout << "I can go " << myMilesEstimator.getMilesLeft() << " more miles." << endl;
```

该代码的输出如下：

I can go 40 miles.

为了让模拟器更有趣，你可能引入不同类型的车辆，也许是效率汽车。现有的 `MilesEstimator` 假设所有汽车每加仑油行驶 20 英里，但该值是从特定方法返回的，因此派生类可以重写它。派生类的定义如下：

```cpp
class EfficientCarsEstimator : public MilesEstimator
{
private:
    virtual int getMilesPerGallon() const override { return 35; }
}
```

通过重写这个私有方法，新类完全改变了现有、未修改的公共方法的行为。基类中的 `getGallonsLeft()` 方法会自动调用被重写的私有 `getMilesPerGallon()` 方法。使用新类的示例所示：

```cpp
EfficientCarsEstimator myEfficientEstimator;
myEfficientEstimator.setGallonsLeft(2);
cout << "I can go " << myEfficientEstimator.getMilesLeft() << " more miles." << endl;
```

这一次，输出反映了重写后的功能：

I can go 70 miles.

> 注意：重写 `private` 和 `protected` 方法是改变类功能而无需进行重大重构的好方法。

### 基类方法有默认参数

派生类和基类可以有不同的默认参数，但参数取决于变量的声明类型，而不是底层对象。以下是一个派生类在重写方法中提供不同默认参数的简单示例：

```cpp
class Super {
  public:
    virtual void go(int i = 2) {
      cout << "Super's go with i=" << i << endl;
    }
};

class Sub : public Super {
  public:
    virtual void go(int i = 7) override {
      cout << "Sub's go with i=" << i << endl;
    }
};
```

如果在 `Sub` 对象上调用 `go()`，将执行 `Sub` 版本的 `go()` 并使用默认参数 7。如果在 `Super` 对象上调用 `go()`，将执行 `Super` 版本的 `go()` 并使用默认参数 2。然而，如果在指向 `Sub` 对象的 `Super` 指针或 `Super` 引用上调用 `go()`，将调用 `Sub` 版本的 `go()`，但它将使用默认参数 2。这种行为在下面的示例所示：

```cpp
Super mySuper;
Sub mySub;
Super* pSuper = &mySub;
Super& rSuper = mySub;
mySuper.go();    // Super's go with i=2
mySub.go();      // Sub's go with i=7
pSuper->go();    // Super's go with i=2
rSuper.go();     // Super's go with i=2
```

该代码的输出是：

Super's go with i=2
Sub's go with i=7
Super's go with i=2
Super's go with i=2

> 注意：默认参数在编译时绑定，而不是在运行时。

### 基类方法有不同的默认参数

派生类和基类可以有不同的默认参数，但参数取决于变量的声明类型，而不是底层对象。以下是一个派生类在重写方法中提供不同默认参数的简单示例：

（等待，提供的 OCR 文本在末尾似乎重复或碎片化了。我已根据提供的 C++ 上文重构了逻辑流。）

### 派生类中的拷贝构造函数和赋值运算符

第 8 章提到，当类中存在动态分配内存时，提供拷贝构造函数和赋值运算符被认为是一种良好的编程实践。在定义派生类时，你需要小心拷贝构造函数和 `operator=`。

如果你的派生类没有任何需要非虚拷贝构造函数或 `operator=` 的特殊数据，通常是指针，那么无论基类是否拥有这些内容，你都不需要定义它们。如果派生类遗漏了拷贝构造函数或 `operator=`，编译器将为派生类中的数据成员提供默认的拷贝构造函数或 `operator=`，并使用基类的拷贝构造函数或 `operator=` 来处理基类中的数据成员。

相反，如果你**确实**在派生类中指定了拷贝构造函数，你需要显式地调用父类的拷贝构造函数，如下代码所示。如果你不这样做，对象的父类部分将使用默认构造函数，而不是拷贝构造函数。

```cpp
class Super {
  public:
    Super();
    Super(const Super& inSuper);
};

class Sub : public Super
{
  public:
    Sub();
    Sub(const Sub& inSub);
};

Sub::Sub(const Sub& inSub) : Super(inSub) {}
```

同样，如果派生类重写了 `operator=`，几乎总是必须调用父类版本的 `operator=`。唯一你不需要这样做的情况是：由于某些诡异的原因，你只想在发生赋值时赋值对象的一部分。以下代码展示了如何从派生类调用父类的赋值运算符：

```cpp
Sub& Sub::operator=(const Sub& inSub) {
  if (&inSub == this) {
    return *this;
  }
  Super::operator=(inSub); // 调用父类的 operator=.
  // 对派生类进行必要的赋值。
  return *this;
}
```

### 关于 virtual 的真相

当你在本章前面的部分第一次遇到方法重写时，我告诉过你只有虚方法可以被重写。我必须正确添加该限定符的原因是：如果一个方法不是虚的，你仍然可以尝试重写它，但它会在微妙之处产生错误。

### 隐藏而非重写

以下代码显示了一个基类和一个派生类，每个类都有一个方法。派生类试图重写基类中的方法，但该方法在基类中并未声明为虚方法。

```cpp
class Super {
public:
    void go() { cout << "go() called on Super" << endl; }
};

class Sub : public Super
public:
    void go() { cout << "go() called on Sub" << endl; }
};
```

在 `Sub` 对象上调用 `go()` 方法最初看起来可以工作。

```cpp
Sub mySub;
mySub.go();
```

此调用的输出如预期的是 `go() called on Sub`。然而，由于该方法不是虚的，它实际上并没有被重写，而是被隐藏了。`Sub` 类创建了一个也名为 `go()` 的方法。要证明这一点，只需在 `Super` 指针或引用的范围内调用该方法即可。

```cpp
Sub mySub;
Super& ref = mySub;
ref.go();
```
