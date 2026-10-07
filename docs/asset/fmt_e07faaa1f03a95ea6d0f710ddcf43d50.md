
除了类之外，`final`也可以用于成员函数以控制多态行为。这将在第11课“多态性”中讨论。

> 鸭嘴兽会游泳，但它不是鱼。因此，在列表10.10中，为了复用现有的`Fish::Swim()`函数，你并没有从`Fish`继承`Platypus`。在做设计决策时，不要忘记公共继承也应该表示一种“是”的关系。不应该为了实现代码复用相关的目标而盲目使用。这些目标可以通过其他方式实现。

## 问答

- 派生类（derived class）和子类（subclass）的区别是什么？
- 本质上没有。两者都用于表示基类的类。
- 它可以访问基类的私有成员吗？不能。编译器始终确保执行限制限制的访问符。无论继承如何，类的私有成员都无法在类外部访问。此规则的异常适用于为为（friend）的类和函数。

## 工作坊

工作坊提供了测试题来帮助巩固你对涵盖内容的理解，并提供了练习让你获得所学知识的。在检查附录E中的答案之前，尝试回答测试和练习，并在继续之前确保理解答案。

- 我希望某些基类成员可以被派生类访问，但不在类外部访问。我应该使用什么访问符？
- 如果我将派生类对象作为参数传递给一个按值接收基类参数的函数，会发生什么？
- 我应该倾向哪一个？私有继承还是组合？
- `using`关键字在继承层次中如何帮助我？
- `Derived`从`Base`继承私有成员。`SubDerived`从`Derived`继承公共成员。`SubDerived`可以访问`Base`的公共成员吗？

## 练习

- 如列表10.10所示，`Platypus`类构造函数的调用顺序是怎样的？
- 展示`Polygon`类、`Triangle`类和`Shape`类是如何相互相关的。
- `class D2`继承自`class D1`，后者继承自`class Base`。为了继续访问`Base`中的公共成员，你会使用什么访问符，并在哪里使用？
- 该代码片段的继承性质是什么：
```cpp
class Derived: Base
  // ... Derived members
};
```
- 错误排除：这段代码中的问题是：
```cpp
class Derived: public Base
  // ... Derived members
};

void SomeFunc (Base value)
{
  // ...
};
```

# 第11课

## 多态

在学习了继承的基础、创建了继承层次结构，并理解了公继承本质上是在模拟“是一个是”（is-a）关系之后，是时候通过学习这些知识来攻克面向对象编程的圣杯：多态了。

在本节中，你将了解到：

- 多态的真正含义
- 虚函数的作用以及如何使用它们
- 什么是抽象基类以及如何声明它们
- 虚继承的含义以及你何时需要它

# 多态的基础

“Poly”在希腊语中是“多”，“morph”意味着“形式”。多态是面向对象语言的一种特性，允许不同类型的对象以相似的方式被对待。本节重点关注通过C++继承层次实现的多态行为，也称为子类型多态。

## 多态行为的性

在第10节“实现继承”中，你发现了金枪鱼（Tuna）和鲤鱼（Carp）如何从鱼（Fish）继承公方法`Swim()`，如列表10.1所示。然而，金枪鱼和鲤鱼都可能提供自己的`Tuna::Swim()`和`Carp::Swim()`方法，使它们成为会游泳者。但是，由于它们每一个也是“鱼”，如果一个拥有金枪鱼实例的用户使用基类类型来调用`Fish::Swim()`，他执行的将仅是通用的`Fish::Swim()`部分，而不是`Tuna::Swim()`，即使该基类`Fish`是是金枪鱼的一部分。这个问题在列表11.1中得到了演示。

> 本节中的所有代码示例都已精简到解释相关主题所需的最核心部分，并尽可能减少了代码行数以提高可读性。

在编程时，你应该正确地编写类并创建有意义的继承层次结构，同时考虑到应用程序的设计和目的。

### 列表11.1 使用属于金枪鱼的基类Fish实例调用方法

```cpp
#include <iostream>
1: using namespace std;
2:
3: class Fish
4: {
5: public:
6:   void Swim()
7:   {
8:     cout << "Fish swims!" << endl;
9:   }
10: };
```

```cpp
12: class Tuna:public Fish
13: {
14:     public:
15:     // override Fish::Swim
16:     void Swim()
17:     {
18:         cout << "Tuna swims!" << endl;
19:     }
20: }
22: void MakeFishSwim(Fish& inputFish)
23: {
24:     // calling Fish::Swim
25:     inputFish.Swim();
26: }
27: 
28: int main()
29: {
30:     Tuna myDinner;
31: 
32:     // calling Tuna::Swim
33:     myDinner.Swim();
34: 
35:     // sending Tuna as Fish
36:     MakeFishSwim(myDinner);
37: 
38:     return 0;
39: }
```

### 输出

```
Tuna swims!
Fish swims!
```

### 分析

`class Tuna`特化了`class Fish`，`main()`在第33行直接调用了`Tuna::Swim()`，同时也重写了`Fish::Swim()`，并将`myDinner`（类型为`Tuna`）作为参数传递给`MakeFishSwim()`，而该函数根据第22行的声明将其解释为引用`Fish&`。换句话说，`MakeFishSwim(Fish&)`并不关心发送的对象是否是金枪鱼，它将其视为`Fish`处理，并调用了`Fish::Swim()`。因此，输出的第二行表示同一个对象`Tuna`产生了输出：一个`Fish`的输出，而不是指示其有任何特化（这也可以是鲤鱼）。

用户理想上的期望是，即使调用的是`Fish::Swim()`，类型为`Tuna`的对象也表现得像金枪鱼。也就是说，当第25行调用`inputFish::Swim()`时，他期望执行`Tuna::Swim()`。这种已知类`Fish`对象可以表现为其实际类型（即派生类`Tuna`）的行为，可以通过将`Swim()`声明为虚函数来实现。

## 使用虚函数实现的多态

你通过指针`Fish*`或引用`Fish&`访问类型为`Fish`的对象。该对象可能仅被实例化为`Fish`，也可能是自`Fish`的`Tuna`或`Carp`。你并不知道（也不关心）。你这样使用指针或引用调用`Swim()`：

```cpp
Fish->Swim();
inputFish.Swim();
```

你期望当对象属于`Tuna`时它像金枪鱼一样游泳，属于`Carp`时它像鲤鱼一样游泳，在未作为`Tuna`或`Carp`等派生类实例化时像匿名`Fish`一样游泳。你可以通过在基类`Fish`中将`Swim()`声明为虚函数来实现：

```cpp
class Base
{
    virtual void Swim();
};
class Derived
{
};
```

使用`virtual`关键字意味着编译器确保调用请求的基类方法的重写版本。因此，如果`Swim()`被声明为虚函数，调用`inputFish.Swim()`（类型为`Fish&`）将如列表11.2所示导致`Tuna::Swim()`。

### 列表11.2 将`Fish::Swim()`声明为虚函数

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Fish
4: {
5: public:
6:   virtual void Swim()
7:   {
8:       cout << "Fish swims!" << endl;
9:   }
10: };
11: 
12: class Tuna:public Fish
13: {
14:     public:
15:         // override Fish::Swim
16:         void Swim()
17:     {
18:             cout << "Tuna swims!" << endl;
19:         }
20: };
21: 
22: class Carp:public Fish
23: {
24:     public:
25:         // override Fish::Swim
26:         void Swim()
27:     {
28:             cout << "Carp swims!" << endl;
29:         }
30: };
31: 
32: void MakeFishSwim(Fish& inputFish)
33: {
34:     // calling Fish::Swim
35:     inputFish.Swim();
36: }
37: 
38: int main()
39: {
40:     Tuna myDinner;
41: 
42:     // calling Tuna::Swim
43:     myDinner.Swim();
44: 
45:     // sending Tuna as Fish
46:     MakeFishSwim(myDinner);
47: 
48:     return 0;
49: }
```

### 输出

```
Tuna swims!
Fish swims!
```

### 分析

函数`FishSwim(Fish&)`的实现自11.1以来没有变化。但输出完全不同。由于重写版本的存在，`Swim()`没有被调用。这就是多态：将不同的鱼视为共同类型，确保执行正确的派生实现。

## 虚析构函数的需要

列表11.1演示的特性有一个更阴险的一面——故意调用派生类实例的基类功能。当函数调用`delete`时会发生什么？

### 列表11.3 在`Base*`上调用`delete`的函数

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Fish
4: {
5: public:
6:     void Swim()
7:     {
8:         cout << "Fish swims!" << endl;
9:     }
10: };
11: 
12: class Tuna:public Fish
13: {
14:     public:
15:         // override Fish::Swim
16:         void Swim()
17:     {
18:             cout << "Tuna swims!" << endl;
19:         }
20: };
23:  ~Tuna()
24:  {
25:     cout << "Destroyed Tuna" << endl;
26:  }
27: };
28: 
29: void DeleteFishMemory(Fish* pFish)
30:  {
31:     delete pFish;
32:  }
33: 
34: int main()
35:  {
36:     cout << "Allocating a Tuna on the free store:" << endl;
37:     Tuna* pTuna = new Tuna;
38:     cout << "Deleting the Tuna: " << endl;
39:     DeleteFishMemory(pTuna);
40: 
41:     cout << "Instantiating a Tuna on the stack:" << endl;
42:     Tuna myDinner;
43:     cout << "Automatic destruction as it goes of scope: " << endl;
44: 
45:     return 0;
46:  }
```

### 输出

```
Allocating a Tuna on the free store:
Constructed Fish
Constructed Tuna
Deleting the Tuna:
Destroyed Fish
Instantiating a Tuna on the stack:
Constructed Fish
Constructed Tuna
Automatic destruction as it goes of scope:
Destroyed Tuna
Destroyed Fish
```

### 分析

`main()`在第37行使用`new`在自由存储上创建了一个`Tuna`实例，并在第39行调用服务函数`DeleteFishMemory()`后立即释放了分配的内存。为了对比，另一个`Tuna`实例在第42行作为局部变量`myDinner`在栈上创建，并在`main()`结束时离开作用。输出是由`Fish`和`Tuna`类的构造函数和析构函数中的`cout`语句产生的。

# 第11课：多态

由于使用了`new`在自由堆上构造，Tuna的析构函数在`delete`时没有被调用，而是调用了Fish的析构函数。这与本地成员`myDinner`的构造和析构形成了鲜明对比，所有的构造函数和析构函数都会被调用。第10课在讲座10.7中演示了继承体系中类的正确构造和析构顺序，显示所有析构函数都需要被调用，包括`~Tuna()`。显然，有些不对。

这个缺陷意味着，如果使用`new`在自由堆上实例化类型为`Base*`的派生类指针，其析构函数就不会被调用。这可能导致资源未释放、内存泄漏等，是不容忽视的问题。

为了避免这个问题，你可以如列表11.4所示使用虚析析构函数。

### 列表11.4 使用虚析析构函数确保在删除Base*类型指针时调用派生类的析构函数

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Fish
4: {
5: public:
6: Fish()
7: {
8:   cout << "Constructed Fish" << endl;
9: }
10: virtual ~Fish() // 虚析构函数;
11: {
12:   cout << "Destroyed Fish" << endl;
13: }
14: };
15:
16: class Tuna:public Fish
17: {
18: public:
19: Tuna()
20: {
21:   cout << "Constructed Tuna" << endl;
22: }
23: ~Tuna()
24: {
25:   cout << "Destroyed Tuna" << endl;
26: }
27: };
28:
29: void DeleteFishMemory(Fish* pFish)
30: {
31:   delete pFish;
32: }
33:
34: int main()
35: {
36:   cout << "Allocating a Tuna on the free store:" << endl;
37:   Tuna* pTuna = new Tuna;
38:   cout << "Deleting the Tuna: " << endl;
39:   DeleteFishMemory(pTuna);
40:
41:   cout << "Instantiating a Tuna on the stack:" << endl;
42:   Tuna myDinner;
43:   cout << "Automatic destruction as it goes out of scope: " << endl;
44:
45:   return 0;
46: }
```
