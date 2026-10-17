
## 18.3.4. 虚继承

虽然类的派生列表可能不包含同一个一个基类，但类可以间接继承同一个基类。

举个例子，IO 库 `istream` 和 `o` 每个都继承一个名为 `basic_ios` 的公共基类。该类持有流的缓冲区并管理流的状态。`iostream` 既可以读取也可以写入流，它直接继承自 `istream` 和 `o`。由于两者都继承 `basic_ios`，`iostream` 继承了两次，一次通过 `istream`，一次通过 `o`。

默认情况下，派生对象包含与其派生链中的每个类对应的进程。如果相同的基类在派生中出现多次，派生对象将拥有该类型的多个一个对象。

这种默认对于像 `istream` 这样的类是不行的。`istream` 对象希望在读取和写入时使用同一个缓冲区，并且希望状态反映输入和输出操作。如果 `istream` 对象有两个 `basic_ios` 类的副本，这种共享是不可能的。

在 C++ 中，我们通过使用虚继承解决这类问题。虚继承让类指定它愿意共享其基类。共享的类对象被称为虚基类。无论相同的虚基类在继承层次结构中出现多少次，派生对象只包含一个，一个共享的子类对象。

# 不同的 Panda 类

过去，关于 `panda` 是否属于或 `bear` 家族是有讨论的。为了反映这一点，我们可以让 `Panda` 继承 `Bear` 和 `Raccoon`。为了避免给 `Panda` 带来两个 `ZooAnimal` 基部分，我们将定义 `Bear` 和 `Raccoon` 虚继承 `ZooAnimal`。图 18.3 展示了我们的新的层次结构。

![](img/3a7e14b77396239ca7166fc2adb32975_993_0.png)

图 18.3. 虚继承 Panda 结构

观察我们新的层次结构，我们将注意到虚继承的一个非直觉方面。虚派生必须在它出现之前做出。例如，在我们的类中，虚继承的需求只在我们定义 `Panda` 时产生。然而，如果 `Bear` 和 `Raccoon` 没有在从 `ZooAnimal` 派生时指定虚，那么 `Panda` 类的设计者就倒霉了。

`virtual`（虚函数）很少引起任何问题。通常，使用虚类继承的类层次结构是由一个个人或一个项目设计小组一次性设计的。独立开发一个类，并需要在其其中一个基类中使用虚基类，且该新基类的开发者无法更改现有的层次结构，这种情况是极其罕见的。

> 注意
> 虚派生影响后续派生自具有虚基类的类；它不会影响派生类本身。

## 使用虚基类

我们通过在派生列表列表中包含 `virtual` 关键字来指定基类是虚的：

点击此处查看代码图片

```
// public 和 virtual 关键字的顺序并不重要

class Raccoon : public virtual ZooAnimal { /* ... */ };

class Bear : public virtual ZooAnimal { /* ... */ };
```

这里将 `ZooAnimal` 变成了 `Bear` 和 `Raccoon` 的虚基类。
`virtual` 标识符表示愿意在后续的派生类中共享命名基类的单个实例。对用作虚基类的类没有特殊限制。

继承一个具有虚基类的类时，我们不需要做任何特殊操作：

点击此处查看代码图片

```
class Panda : public Bear, public Endangered {

    public Raccoon,

};
```

这里 `Panda` 通过它的 `Raccoon` 和 `Bear` 基类继承了 `ZooAnimal`。然而，由于这些类是虚继承自 `ZooAnimal` 的，`Panda` 只有一个 `ZooAnimal` 子部分。

## 支持到基类的正常转换

无论基类是否为虚，派生类对象都可以通过指向可访问基类类型的指针或引用（像通常一样）进行操作。例如，以下基类转换都是合法的：

点击此处查看代码图片

```
void dance(const Bear&);

void rummage(const Raccoon&, const ZooAnimal&);

stream& operator<<(ostream&, yin_yang);

dance(yin_yang); // ok：将 Panda 对象作为 Bear 传递

rummage(yin_yang); // ok：将 Panda 对象作为 Raccoon 传递

cout << yin_yang; // ok：将 Panda 对象作为 ZooAnimal 传递
```

## 虚基类成员的可见性

由于每个共享虚基类对应一个共享子对象，基类中的成员可以直接且无歧义地访问。此外，如果虚基中的某个成员仅在一个派生中被重写，那么该被重写的成员可以可以直接访问。如果该成员被多个派生重写，则派生类必须定义它自己的版本。

例如，假设类 `B` 定义了一个名为 `x` 的成员；类 `D1` 继承自 `B`，而类 `D` 继承自 `D1` 和 `D2`。从 `D` 的作用范围内，`x` 通过它的两个基类都是可见的。如果我们通过 `D` 对象使用 `x`，有三种可能性：

- 如果 `x` 未在 `D1` 或 `D2` 中定义，它将被解析为 `B` 中的成员；这里没有歧义。一个 `D` 对象只包含 `x` 的一个实例。
- 如果 `x` 是 `B` 的成员，同时也是 `D1` 或 `D2`（但不是两者）的成员，则再次没有歧义——派生类的版本优先。
- 如果 `x` 在 `D1` 和 `D2` 中都定义，那么直接访问该成员将产生歧义。

在虚继承层次结构中，此类歧义由派生类提供该成员的自己的实例来解决。

> 练习题 18.3.4
> **练习题 18.28：**给定下面的类层次结构，在 `VMI` 类内部哪些继承的成员不需要限定即可访问？哪些需要限定？请说明你的理由。

点击此处查看代码图片

```
struct Base {

    void bar(int); // 默认 public

protected:

    int ival;

};

struct Derived1 : virtual public Base {

    void bar(char); // 默认 public

void foo(char);

protected:

  char cval;

};

struct Derived2 : virtual public Base {

  void foo(int); // 默认 public

protected:

  int ival;

  char cval;

};

class VMI : public Derived1, public Derived2 { };
```

## 构造函数与虚继承

在虚派生中，虚基由最派生的构造函数初始化。在我们的示例中，创建一个 `Panda` 对象，`Panda` 构造函数控制 `ZooAnimal` 基类的初始化。

为了理解这条规则，考虑如果应用普通初始化会发生什么。在这种情况下，虚基可能会被初始化多次。在 `ZooAnimal` 示例中，如果应用普通初始化，`Bear` 和 `Raccoon` 将初始化 `ZooAnimal` 部分。

当然，层次结构中的每个类都可能是“最派生”对象。只要我们能创建派生自虚基的独立对象，该类的构造函数必须初始化其虚基。在我们的示例中，当创建 `Bear`（或 `Raccoon`）时，没有进一步的派生类型。在这种情况下，`Bear`（或 `Raccoon`）构造函数直接初始化 `ZooAnimal`：

点击此处查看代码图片

```
Bear::Bear(std::string name, bool onExhibit) {

  ZooAnimal(name, onExhibit, "Bear")

}

Raccoon::Raccoon(std::string name, bool onExhibit) {

  ZooAnimal(name, onExhibit, "Raccoon")

}
```

当创建 `Panda` 时，它是最派生类型并初始化共享 `ZooAnimal` 基。尽管 `ZooAnimal` 不是 `Panda` 的直接基类，`Panda` 构造函数也会初始化它：

点击此处查看代码图片

```
Panda::Panda(std::string name, bool onExhibit) {

  ZooAnimal(name,onExhibit, "Panda")

  Bear(name,onExhibit),

  Raccoon(name,onExhibit),

  Endangered(Endangered::critical),

  sleeping(false)

}
```

## 虚继承对象的构造

具有虚基的对象的构造顺序与普通顺序略有不同：对象的虚基部分首先初始化，使用最派生类构造函数提供的初始化器。一旦对象的虚基部分构造完成，直接基部分按照它们在派生列表中出现的顺序进行构造。

例如，当创建一个 `Panda` 对象时：

- 首先构造（虚基类）`ZooAnimal` 部分，使用 `Panda` 构造函数指定的初始化器。
- 接着构造 `Bear` 部分。
- 接着构造 `Raccoon` 部分。
- 接着构造第三直接基 `Endangered`。
- 最后构造 `Panda` 部分。

如果 `Panda` 构造函数没有显式初始化 `ZooAnimal` 基类，则使用 `ZooAnimal` 的默认构造函数。如果 `ZooAnimal` 没有默认构造函数，则代码将报错。

> 注意 虚基类无论出现在继承层次结构的什么位置，总是先于非虚基类进行构造。

## 构造函数和析构函数的顺序

一个类可以有多个虚基类。在这种情况下，虚子对象按照它们在派生列表中从左到右顺序构造。例如，在下面的奇特 `TeddyBear` 派生中，有两个虚基类：`ToyAnimal`（直接虚）和 `ZooAnimal`（它是 `Bear` 的虚基类）：

点击此处查看代码图片

```
class Character { /* ... */ };

class BookCharacter { public Character { /* ... */ }; };

class ToyAnimal { /* ... */ };

class TeddyBear : public BookCharacter,

    public Bear, public virtual ToyAnimal

    { /* ... */ };
```

按照声明顺序检查直接基类以确定是否存在虚基类。如果是，则构造虚基，然后按照声明顺序构造非虚类。因此，创建一个 `TeddyBear`，构造函数按以下顺序调用：

点击此处查看代码图片

```
ZooAnimal(); // Bear 的虚基类

ToyAnimal(); // 直接基类

Character(); // 间接基类的第一个非虚基类

BookCharacter(); // 第一非虚基类

Bear(); // 第二非虚基类

TeddyBear(); // 最派生类
```

相同的顺序被用于生成的拷贝构造函数和移动构造函数，成员在赋值运算符中按此顺序赋值。按照通常，对象按照构造顺序的反序进行析构。`TeddyBear` 将首先析构，最后析构 `ZooAnimal` 部分。

## 练习题 18.3.4/18.5

**练习题 18.28：**给定下面的类层次结构，在 `VMI` 类内部哪些继承的成员不需要限定即可访问？哪些需要限定？请说明你的理由。

点击此处查看代码图片

```
struct Base {

    void bar(int); // 默认 public

protected:

    int ival;

};

struct Derived1 : virtual public Base {

    void bar(char); // 默认 public

void foo(char);

protected:

  char cval;

};

struct Derived2 : virtual public Base {

  void foo(int); // 默认 public

protected:

  int ival;

  char cval;

};

class VMI : public Derived1, public Derived2 { };
```

## 练习题 18.3.5

**练习题 18.29：**给定类层次结构：

点击此处查看代码图片

```
class Class { ... };

class Base : public Class { ... };

class D1 : virtual public Base { ... };

class D2 : virtual public Base { ... };

class MI : public D1, public D2 { ... };

class Final : public MI, public Class { ... };
```

- (a) `Final` 对象上构造函数和析构函数的运行顺序是什么？
- (b) `Final` 对象有多少个 `Base` 部分？有多少个 `Class` 部分？
- (c) 以下哪些赋值是编译时错误？

```
Base *pb; Class *pc; MI *pmi; D2 *pd2;

a)** pb = new Class;

**(b)** pc = new Final;

**(c)** pmi = pb;

**(d)** pd2 = pmi;
```
