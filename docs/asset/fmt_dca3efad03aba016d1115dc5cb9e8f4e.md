
- C++ 还允许你使用类型转换运算符 `dynamic_cast` 来查询一个是否为 `Derived*` 类型的指针 `Base*`，然后根据查询结果执行条件分支。

这被称为运行时类型识别（RTTI），尽管大多数 C++ 编译器都支持它，但应该避免使用。这是因为需要知道基类指针背后的派生类对象的类型通常被认为是糟糕的编程实践。

RTTI 和 `dynamic_cast` 将将在第 13 节“转换运算符”中讨论。

## 抽象基类与纯虚函数

不能实例化的基类称为抽象基类。这种基类只实现一个目的：即被派生。C++ 允许你使用纯虚函数来创建抽象基类。

当一个方法具有如下所示声明时，它被称为纯虚方法：

```cpp
class AbstractBase
{
public:
    virtual void DoSomething() = 0; // 纯虚方法
};
```

该声明本质上告诉编译器，`DoSomething()` 需要由派自 `AbstractBase` 的类来实现：

```cpp
class Derived: public AbstractBase
{
public:
```

## 多态性的基础

```cpp
void DoSomething() // 纯虚方法
{
    cout << "Implemented virtual function" << endl;
}
```

因此，`AbstractBase` 类所做的是强制 `Derived` 类为虚方法 `DoSomething()` 提供实现。这种基类可以强制派生自它的类支持具有特定名称和签名的方法，这就是接口的功能。再次想象一条鱼（Fish）。想象一条游得不快的金枪鱼（Tuna），金枪鱼没有重写 `Fish::Swim()`。这是一个失败的实现且是一个缺陷。将 `Fish` 类设为带有 `Swim` 纯虚函数的抽象基类，可以确保 `Tuna` 派生了 `Tuna::Swim()` 并游得像金枪鱼，而不仅仅像任何鱼。参见列表 11.6。

### 列表 11.6 将 Fish 作为金枪鱼和鲤鱼的抽象基类

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Fish
4: {
5: public:
6:     // 定义纯虚函数 Swim
7:     virtual void Swim() = 0;
8: };
9:
10: class Tuna:public Fish
11: {
12: public:
13:     void Swim()
14:     {
15:         cout << "Tuna swims fast in the sea!" << endl;
16:     }
17: };
18:
19: class Carp:public Fish
20: {
21:     void Swim()
22:     {
23:         cout << "Carp swims slow in the lake!" << endl;
24:     }
25: };
26:
27: void MakeFishSwim(Fish&inputFish)
28: {
29:     inputFish.Swim();
30: }
```

### 列表 11.6 续

```cpp
30: }
31:
32: int main()
33:
34: // Fish my; // 失败，不能实例化抽象类
35: Carp myLunch;
36: Tuna myDinner;
37:
38: MakeFishSwim(myLunch);
39: MakeFishSwim(myDinner);
40:
41: return 0;
42: }
```

### 输出

Carp 在湖中游得慢！

Tuna 在海中游得快！

### 分析

`main()` 中的第 34 行（注释掉）意义重大。它说明编译器不允许你创建 `Fish` 的实例。它期望一个具体的对象，例如 `Fish` 的特化类——这在现实世界的安排是合理的。由于第 7 行声明的虚函数 `Fish::Swim()`，`Tuna` 和 `Carp` 都被强制实现 `Tuna::Swim()`。第 27-30 行的 `MakeFishSwim(Fish&)` 说明，如果不能实例化基类，你可以将其作为引用或指针。抽象基类是一种很好的机制，用于声明你期望所有派生类实现的函数。如果派自 `Fish` 的类没有实现 `Fish::Swim()`，编译将失败。

## 注意事项

| 抽象基类通常就是 ABC |

| ABC 对你的程序施加某些设计限制 |

## 使用虚继承解决菱问题

在第 10 节中，你看到了鸭嘴兽（platypus）的奇特情况，它既是哺乳动物又是鸟类还是爬行动物。这是一个 `Platypus` 类派自 `Mammal`、`Bird` 和 `Reptile` 的例子。然而，这些都派自一个更通用的 `Animal` 类，如图 11.2 所示。

![鸭嘴兽](img/fd0f923cb963a04201153b21581c321_0.png

当你实例化 `Platypus` 时会发生什么？一个 `Platypus` 会实例化多少个 `Animal` 实例？列表 11.7 答了这个问题。

### 列表 11.7 检查一个 Platypus 对应的 Animal 类实例数量

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Animal
4: {
5: public:
6:
   Animal()
7:     {
8:         cout << "Animal constructor" << endl;
9:     }
10:
11:  // 示例方法
12:  int Age;
13: };
14:
15: class Mammal:public virtual Animal
16: {
17: };
18:
19: class Bird:public virtual Animal
20: {
21: };
22:
23: class Reptile:public virtual Animal
24: {
25: };
26:
27: class Platypus:public Mammal, public Bird, public Reptile
28: {
29: public:
30:     Platypus()
31:     {
32:         cout << "Platypus constructor" << endl;
33:     }
34: }
35:
36: int main()
37: {
38:     Platypus duckBilled;
39:
40: // 取消取消注释以编译
41:     duckBilled.Age = 25; // 编译错误
42:
43:     return 0;
44: }
```

### 使用虚继承解决菱问题

#### 输出

Animal 构造函数

Animal 构造函数

Platypus 构造函数

#### 分析

如输出所示，由于多继承，每个 `Platypus` 实例都会创建三个 `Animal` 实例（如第 38 行），你得到了编译错误，仅因为编译器不知道你想设置 `Mammal::Age`、`Bird::Age` 还是 `Reptile::Age`。显然，`platypus` 应该只有一个 `Age`。解决方案是虚继承。如果你期望一个派生类被用作基类，可能使用关键字定义它与基类的关系是个好主意：

```cpp
class Derived1: public virtual Base
  // ... 成员和函数
};
class Derived2: public virtual Base
  // ... 成员和函数
};
```

# 第 11 节：多态

### 列表 11.8 展示继承层次中的关键字如何帮助限制基类 Animal 的数量为一个

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Animal
4: {
5: public:
6:   Animal()
7:     {
8:         cout << "Animal constructor" << endl;
9:     }
10:
11:  // 示例方法
12:  int Age;
13: };
14:
15: class Mammal:public virtual Animal
16: {
17: };
18:
19: class Bird:public virtual Animal
20: {
21: };
22:
23: class Reptile:public virtual Animal
24: {
25: };
26:
27: class Platypus:public Mammal, public Bird, public Reptile
28: {
29: public:
30:     Platypus()
31:     {
32:         cout << "Platypus constructor" << endl;
33:     }
34: }
35:
36: int main()
37: {
38:     Platypus duckBilled;
39:
40:     // 没有编译错误，因为只有一个 Animal::Age
41:     duckBilled.Age = 25;
42:
43:     return 0;
44: }
```

## 使用虚继承解决菱形问题

### 输出

Animal 构造函数

Platypus 构造函数

### 分析

与之前的列表 11.7 输出进行快速对比，你会发现 Animal 类的实例数量减少到了一个，这最终反映了实际上只构造了一个 Platypus。这是因为在 Mammal（哺乳动物类）、Bird（鸟类类）和 Reptile（爬行动物类）类之间的关系中使用了 `virtual` 关键字，确保了当这些类被归类在 Platypus 之下时，公共基类 Animal 只存在一个实例。这解决了许多问题；其中之一是第 41 行，现在不需要解析歧义即可编译，如列表 11 所示。

| 在包含两个或多个继承自共同基类的继承层次结构中引起的问题（导致在没有虚继承的情况下需要解析歧义），被称为“菱形问题”。 |

| “菱形”这个名称可能灵感来源于类图呈现的形状（可视化图 11.2，通过直线和斜线将 Platypus 与 Animal 通过 Mammal、Bird 和 Reptile 连接起来，即可看到一个菱形）。 |

C++ 中的 `virtual` 关键字经常在不同的上下文中用于不同的目的。（我最好的猜测是有人想节省发明一个新关键字的时间。）以下是总结：

声明为 `virtual` 的函数意味着：在类 Derived1 和 Derived2 之间使用 `virtual` 关键字声明的现有的重写继承关系，意味着另一个继承自 Derived1 和 Derived2 的类 Derived3 在实例化类型 Derived3 时，仍然只会创建一个 Base 的单实例。

因此，同一个 `virtual` 关键字被用于实现两个不同的概念。

## 虚拷贝构造函数？

嗯，章节标题末尾的问号是有理由的。在 C++ 中，技术上是不存在虚拷贝构造函数的。然而，这种功能可以帮助你创建一个 `Base*` 集合（用于静态数组），每个元素都是该类型的特化类：

```cpp
// Tuna, Carp 和 Trout 是继承自基类 Fish 的类
Fish* fishes[3];
Fishes[0] = new Tuna();
Fishes[1] = new Carp();
Fishes[2] = new Trout();
```

当将其赋值给另一个相同类型的数组时，虚拷贝构造函数确保了派生对象的深拷贝，从而确保即使拷贝构造函数是在 `Fish` 类型上操作，Tuna、Carp 和 Trout 也会被拷贝为 Tuna、Carp 和 Trout。

嗯，这是一个很美的梦想。

虚拷贝构造函数是不可能的，因为 `virtual` 关键字在类方法被派生类实现重写的上下文中，指的是关于运行时生成的多态行为。另一方面，构造函数在本质上不是多态的，因为它们只能构造固定类型，因此 C++ 不允许使用虚拷贝构造函数。

尽管如此，还有一种很好的变通方法，即定义你自己的 `clone` 函数，这允许你实现这一点：

```cpp
class Fish
public:
  virtual Fish* Clone() const = 0; // 纯虚函数
};

class Tuna:public Fish
{
  //... 其他成员
public:
  Tuna* Clone() const // 虚拷贝函数
  {
    return new Tuna(*this); // 返回一个副本的 new Tuna
  }
};
```

因此，虚函数 `Clone` 是模拟的虚拷贝构造函数，需要显式调用，如列表 11.9 所示。

### 列表 11.9 支持通过 Clone 函数模拟拷贝构造函数的 Tuna 和 Carp

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Fish
4: {
5:     public:
6:     virtual Fish* Clone() = 0;
7:     virtual void Swim() = 0;
8: };
9:
10: class Tuna: public Fish
11: {
12:     public:
13:     Fish* Clone()
14:     {
15:         return new Tuna(this);
16:     }
17:
18:     void Swim()
19:     {
20:         cout << "Tuna swims fast in the sea" << endl;
21:     }
22: };
23:
24: class Carp: public Fish
25: {
26:     Fish* Clone()
27:     {
28:         return new Carp(this);
29:     }
30:     void Swim()
31:     {
32:         cout << "Carp swims slow in the sea" << endl;
33:     }
34: };
35:
36: int main()
37: {
38:     const int ARRAY_SIZE = 4;
39:     Fish* fishes[ARRAY_SIZE];
40:     fishes[0] = new Tuna();
41:     fishes[1] = new Carp();
42:     fishes[2] = new Tuna();
43:     fishes[3] = new Carp();
44:
45:     for (int i = 0; i < ARRAY_SIZE; ++i)
46:         fishes[i]->Clone();
47:         fishes[i]->Swim();
48:     }
49:     return 0;
50: }
```

# 第 11 课：多态

问 基类是否应该始终有一个虚析构函数？

答 理想情况下是的。只有这样才能确保当有人执行以下代码时

```cpp
Base* pBase = new Derived();
delete pBase;
```

对 `Base*` 类型指针进行 `delete` 操作，如果只有 `~Base()` 被声明为虚函数，会导致调用 `~Derived()` 析构函数。

问 我甚至无法独立实例化它，那么抽象基类（ABC）有什么用呢？

答 ABC 的目的不是作为独立对象被实例化；相反，它总是被派生的。它包含了纯虚函数，定义了派生类需要实现的最小函数蓝图，从而充当接口的角色。

问 给定一个继承层次结构，我需要在所有虚函数的声明处都使用 `virtual` 关键字，还是只需要在基类中使用？

答 只需要有一个虚函数声明就足够了，且该声明必须在基类中。

问 我可以在 ABC 中定义成员函数并拥有成员属性吗？

答 可以的。请记住，你仍然无法实例化 ABC，因为它至少有一个需要由派生类实现的纯虚函数。

## 工作坊

工作坊提供了测验题帮助你巩固对所涵盖内容的理解，并提供了练习让你获得所学知识的经验。在检查附 D 中的答案之前，尝试回答测验和练习题，并在继续下一课之前确保理解了答案。

## 测验

- 1. 你正在为形状——圆形和三角形——希望每个形状都强制实现 `Area()` 和 `Print()` 函数。你会如何做？

- 2. 编译器是否会为所有类创建虚函数表？

- 3. 我的类 `Fish` 有两个公共方法、一个纯虚函数和一些成员属性。它仍然是一个抽象基类吗？

## 练习

- 1. 展示一个继承层次结构，实现测验 1 中针对圆形和三角形的问题。

- 2. 漏洞排查（BUG BUSTERS）：以下代码中的问题是什么：

```cpp
class Vehicle
{
public:
    Vehicle() {}
    ~Vehicle(){}
};
class Car: public Vehicle
{
public:
    Car() {}
    ~Car(){}
};
```

- 3. 在练习 2 的（不）正确代码中，如果这样创建并销毁一个 实例，构造函数和析构函数的执行顺序是怎样的：

```cpp
Vehicle* pMyRacer = new Car;
delete pMyRacer;
```

# 第 12 课

## 运算符类型与运算符重载

`class` 关键字使其能够封装数据和方法，还可以封装便于操作该类对象的运算符。你可以使用这些运算符对类对象执行诸如赋值或加法的操作，类似于你在第 5 课“处理表达式、语句和运算符”中看到的对整数的操作。就像函数一样，运算符也可以是*重载*的。

在这一节中，你将学习：
