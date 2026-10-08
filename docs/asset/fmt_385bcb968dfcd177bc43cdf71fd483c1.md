
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

```cpp
// 像使用普通指针一样使用智能指针！
spData->Display();
(*spData)->Display();
```

```cpp
// 无需担心内存内存
// (智能指针的析构函数会为你完成这一工作)
```

因此，智能指针的行为类似于普通指针（我们现在称之为原始指针），但它们通过其重载的运算符和析构函数提供了实用的功能，以确保动态分配的数据能够被及时销毁。

## 智能指针是如何实现的？

这个问题目前可以简化为：“智能指针 `spData` 是如何像普通指针一样工作的？”答案是：智能指针类重载了解引用用运算符（`*`）和成员选择运算符（`->`），使得程序员可以像使用普通指针一样使用它们。运算符重载在之前的第 12 节“运算符与运算符重载”中讨论过。

除了允许你管理堆上的某种类型对象外，几乎所有的智能指针类都是模板类，包含了其功能的通用实现。作为模板，它们是多功能的，并且可以特化以管理你选择的类型的对象。

列表 26.1 是一个简单智能指针类的示例实现。

### 列表 26.1 智能指针类的最小本质组件

```cpp
0: template <typename T>
1: class smart_pointer
2: {
3:   private:
4:     T* m_pRawPointer;
5:   public:
6:     smart_pointer(T pData) : m_pRawPointer(pData) {} // 构造函数
7:     ~smart_pointer() { delete pData; } // 析构函数
8:
9:     // 拷贝构造函数
10:    smart_pointer(const smart_pointer& anotherSP);
11:    // 拷贝赋值运算符
12:    smart_pointer&operator=(const smart_pointer& anotherSP);
13:
14:    T& operator*(const) const // 解引用运算符
```

### 列表 26.1 继续

```cpp
15:      return *(m_pRawPointer);
16:
17:  }
18:
19:  T* operator->(const    // 成员选择运算符
20:      return m_pRawPointer;
21:
22:  }
23: );
```

## 分析

前面的智能指针类展示了第 14–17 行和 19–22 行中声明的运算符 `*` 和 `->` 的实现，这有助于该类在传统意义上作为“指针”运行。例如，对 `Tuna` 类对象使用智能指针，你可以这样实例化：

```cpp
smartPointer <Tuna> pSmartTuna (new Tuna);
pSmartTuna->Swim();
// 或者：
(*pSmartDog).Swim();
```

这个 `smart_pointer` 类还没有显示或实现任何能让该指针类变得非常智能并使其使用它优于普通指针的优势的功能。如第 7 行所示，构造函数接受一个指针，该指针被保存为智能指针类中的内部指针对象。析构函数释放此指针，实现了自动内存释放。

> 注意
> 使智能指针真正变得“智能”的实现是拷贝构造函数、赋值运算符和析构函数的实现。它们决定了智能指针在跨函数传递、被赋值或超出作用域（即被销毁）时的行为。因此，在查看完整的智能指针实现之前，你应该了解一些智能指针的类型。

## 智能指针的类型

内存资源管理（即所实现的所有权模型）是智能指针类与众不同的地方。智能指针在被拷贝和赋值时决定对资源进行什么操作。最简单的实现通常会导致性能问题，而最快的实现可能不适用于所有应用程序。最后，需要程序员在决定在应用程序中使用它之前理解智能指针是如何工作的。

智能指针的分类实际上是其内存资源管理策略的分类。这些策略包括：

- 深拷贝 `Deep copy`
- 写时复制 `Copy on Write`
- 引用链接 `Reference linked`
- 破坏性拷贝 `Destructive copy`

在学习提供的智能指针之前，让我们简单看看每种策略。

## 深拷贝

使智能指针真正变得“智能”的实现是拷贝构造函数、赋值运算符和析构函数的实现。它们决定了智能指针在跨函数传递、被赋值或超出作用域（即被销毁）时的行为。因此，在查看完整的智能指针实现之前，你应该了解一些智能指针的类型。

在实现深拷贝的智能指针中，每个智能指针都持有对象的副本。当智能指针被拷贝时，所指向的对象也会被拷贝。虽然基于深拷贝的指针似乎没有带来任何优势，但在以下情况下会变得显而易见：

```cpp
// 切片：按值传递对象
// 在这种情况下，智能指针是虚拟的
void Swim(Fish) {
    // ...
}

// 切片：Carp（鲤鱼）不会被切片
Carp f(;);
Swim(f);
```

### 列表 26.2 使用基于拷贝智能指针处理多态对象

类型

```cpp
0: template <typename T>
1: class deepcopy_pointer
2: {
3:   private:
4:     T* mObject;
5:   public:
6:     deepcopy_pointer(T* pData) : mObject(pData) {} // 构造函数


7:     // 拷贝构造函数
8:     deepcopy_pointer(const deepcopy_pointer& anotherSP)
9:     {
10:        if (anotherSP.mObject)
11:            mObject = new T(*anotherSP.mObject);
12:        else
13:            mObject = nullptr;
14:    }
15:
16:    // 拷贝赋值运算符
17:    deepcopy_pointer&operator=(const deepcopy_pointer& anotherSP)
18:    {
19:        if (this != &anotherSP) {
20:            delete mObject;
21:            if (anotherSP.mObject)
22:                mObject = new T(*anotherSP.mObject);
23:            else
24:                mObject = nullptr;
25:        }
26:        return *this;
27:    }
28:
29:    // 析构函数
30:    ~deepcopy_pointer() {
31:        delete mObject;
32:    }
33:
34:    // 解引用运算符
35:    T& operator*(const) const
36:        return *mObject;
37:    }
38:
39:    // 成员选择运算符
40:    T* operator->(const) const
41:        return mObject;
42:    }
43: };
```

分析

前面的智能指针类展示了第 14–17 行和 19–22 行中声明的运算符 `*` 和 `->` 的实现，这有助于该类在传统意义上作为“指针”运行。例如，对 `Tuna` 类对象使用智能指针，你可以这样实例化：

```cpp
smartPointer <Tuna> pSmartTuna (new Tuna);
pSmartTuna->Swim();
// 或者：
(*pSmartDog).Swim();
```

这个 `smart_pointer` 类还没有显示或实现任何能让该指针类变得非常智能并使其使用它优于普通指针的优势的功能。如第 7 行所示，构造函数接受一个指针，该指针被保存为智能指针类中的内部指针对象。析构函数释放此指针，实现了自动内存释放。

## 写时复制

基于深拷贝机制的缺点是性能。这对于某些应用程序可能不是因素，但对于许多其他应用程序，它可能会阻碍程序员使用智能指针。

写时复制（俗称为 `COW`）试图通过在第一次尝试写入之前共享指针来优化智能指针的性能。

`COW` 有其忠实的支持者。对于那些信奉 `COW` 的人来说，实现 `const` 和非 `const` 版本的 `*` 和 `->` 运算符是 `COW` 功能的关键。后者会创建一个副本，而指针实例继续共享源对象。

## 引用计数智能指针

泛而言，引用计数是一种保持对象用户数量计数的机制。当计数减到零时，对象会被释放。因此，引用计数是共享对象而无需复制的一种很好的机制。如果你曾经用过名为 `COM` 的微软技术，引用计数的概念可能至少遇到过你一次。

智能指针在拷贝时，需要增加所涉及对象的引用计数。至少有两种流行的方法来维护这种计数：

- 在被指向的对象中维护引用计数
- 由指针类在共享对象中维护引用计数

# 第 26 节：理解智能指针

`class shared_ptr` 可以在空闲存储（例如一个动态分配的整数）上保留引用计数，并在复制时，拷贝构造函数会增加此值。

因此，引用计数机制使得程序员仅在使用对象时才操作智能指针这变得至关重要。一个管理对象的智能指针和一个指向该对象的原始指针是一个坏主意，因为当智能指针维护的计数减到 0 时，智能指针会（智能地）释放对象，但原始指针会继续指向不再属于你的应用程序的内存。同样，引用计数也会导致其特定情况下特有的问题：两个互相持有指针的对象永远不会被释放，因为它们的循环依赖关系将引用计数保持在至少 1。

## 引用链接智能指针 `Reference-Linked Smart Pointers`

引用链接智能指针不是主动计数对对象的引用次数的；它们只需要知道计数何时归零以便释放它们。

它们之所以被称为引用链接，是因为它们的实现是基于双向链表的。当通过复制现有的智能指针创建新的智能指针时，它会被添加到列表中。当智能指针超出作用范围或被销毁时，它会从该列表中移除该智能指针。引用链接也会受到适用于引用计数指针的循环依赖问题的影响。

## 破坏性拷贝 `Destructive Copy`

破坏性拷贝是一种机制，智能指针在复制时，会将处理的对象的所有权转移到目标，并重置自己：

```cpp
destructive_smart_ptr<SampleClass> pSmartPtr(new SampleClass());

SomeFunc(pSmartPtr); // 所有权转移到 SomeFunc
// 不要再在调用中使用 pSmartPtr 了！
```

尽管这种机制在用起来显然不那么直观，但破坏性拷贝指针提供的优势是，它们确保在任何时间点，只有一个活动指针指向一个对象。因此，它们是从函数中返回指针的良好机制，并且在你可以利用其“破坏性”属性优势的场景中非常有用。

破坏性拷贝指针的实现偏离了标准的、推荐的 C++ 编程技术，列表 26.3 所示。

## 智能指针的类型

### 注意

`std::auto_ptr` 是目前最流行的（取决于你怎么看，也可能是臭名昭著）遵循破坏性拷贝原则的指针。这种智能指针在被传递给函数或复制到另一个指针后就没用了。

`std::auto_ptr` 在 C++11 中已被弃用。相反，你应该使用 `std::unique_ptr`，由于其私有的拷贝构造函数和拷贝赋值运算符，它不能按值传递。它可以作为引用参数传递。

### 列表 26.3 一个破坏性拷贝智能指针

```cpp
0: template <typename T>
1: class destructivecopy_pointer
2: {
3: private:
4:   T* object;
5: public:
6:   destructivecopy_pointer(T* pInput):object(pInput) {
7:   ~destructivecopy_pointer() { delete object; }
8:
9:   // 拷贝构造函数
10:  destructivecopy_pointer(destructivecopy_pointer& source)
11:  {
12:    // 拷贝时获取所有权
13:    object = source.object;
14:    
15:    // 销毁源
16:    source.object = 0;
17:  }
18: 
19:   // 拷贝赋值运算符
20:  destructivecopy_pointer&operator=(destructivecopy_pointer& rhs)
21:  {
22:    if (object != rhs.object)
23:    {
24:      delete object;
25:      object = rhs.object;
26:    rhs.object = 0;
27:    }
28:  }
29: };
30: 
31: int main()
32: {
33:   destructivecopy_pointer<int> pNumber (new int);
34:   destructivecopy_pointer<int> pCopy = pNumber;
35:
36:     // pNumber 现在失效了
37:     return 0;
38: }
```

## 分析

26.3 描述了基于破坏性拷贝的智能指针最重要的部分。第 10-17 行和第 20-28 行分别包含了拷贝构造函数和拷贝赋值运算符。这些函数在拷贝时会使源失效：也就是说，拷贝构造函数将源包含的指针设置为 NULL，从而完成拷贝，这证明了“破坏性拷贝”命名的由来。赋值运算符执行相同的操作。因此，在第 34 行赋值给另一个指针时，指针失效了。这种行为与赋值的操作是背直觉的。

> 注意
> 如列表 26.3 所示，破坏性智能指针实现的关键拷贝构造函数和拷贝赋值运算符实际上非常关注。与 C++ 类不同，这种智能指针类不能让拷贝构造函数和赋值运算符接受引用，因为需要在拷贝后使源失效。这不仅偏离了传统的拷贝构造和赋值语义，还使得使用该智能指针类变得不直觉。预计在拷贝或赋值步骤之后，拷贝源或赋值源会被损坏。智能指针销毁源的特性也使得它们独一无二。

同样，在 Windows 平台上编写这些 COM 应用程序应该开始使用 ATL 框架的有效智能指针类（如 `CComPtr` 和 `CComQIPtr`）来管理它们的 COM 对象，而不是使用原始接口指针。

## 总结

在本节中，你学习了正确的智能指针如何帮助编写使用指针的代码，同时减少与内存分配和对象所有权相关的问题。你还学习了不同的智能指针类型，并了解到在应用中采用智能指针类之前，了解其行为是非常关重要的。你现在知道不应该使用 `std::auto_ptr`，因为它在拷贝或赋值时会使源失效。你学习了从 C++11 开始提供的最新智能指针类——`std::unique_ptr`。

## 问答

- 我需要一个指针向量（vector of pointers）。我应该选择 `auto_ptr` 作为 vector 中的的对象类型吗？
- 作为原则，永远不要使用 `std::auto_ptr`。它已经被废用了。单次拷贝或赋值操作就会导致源对象无法使用。
- 一个类要成为智能指针类总是需要重载哪两个运算符？
- 如下：`operator*` 和 `operator->`。它们帮助像使用普通指针一样使用该类的对象。
- 我有一个应用程序，`Class1` 和 `Class2` 持有指向对方类型对象的成员属性。在这种情况下，我应该使用引用指针（referenced pointer）吗？
- 可能不会，因为循环依赖会导致引用计数无法降为零，从而使类对象一直正确保留在堆中。
- 世界上有多少智能指针？数千个。不，数百万个。你应该只使用那些文档完备且来自可靠来源的智能指针，例如 `Boost`。
- 字符串类（string class）也会在自由存储区（free store）上动态管理字符数组。那么字符串类也是智能指针吗？
- 不的。这些类通常没有同时实现 `operator*` 和 `operator->`，因此不能归类为智能指针。

## 工作坊

工作坊包含了测验题，帮助你巩固对所涵盖内容的理解，并提供了练习以获得使用所学知识的机会。在检查附录 D 中的答案之前，尝试回答测验和练习题，并在进入下一节之前确保你理解了这些答案。

## 测验

- 1. 为你的应用程序编写自己的智能指针时，你应该查看哪里？
- 2. 智能指针会显著减慢你的应用程序吗？
- 3. 引用计数的智能指针可以在哪里存储引用计数数据？
- 4. 引用指针（reference-linked pointers）使用的链表机制应该是单链的还是双链的？

## 练习

- 1. BUG 排除：指出这段代码中的 bug：
```cpp
std::auto_ptr<SampleClass> pObject(new SampleClass());
std::auto_ptr<SampleClass> pAnotherObject(pObject);
pObject->DoSomething();
pAnotherObject->DoSomething();
```
- 2. 使用 `unique_ptr` 类实例化一个继承自 `Fish` 的 `Carp`。将该对象作为 `Fish` 指针传递，并对是否存在切片（slicing）进行注释。
- 3. BUG 排除：指出这段代码中的 bug：
```cpp
std::unique_ptr<Tuna> myTuna (new Tuna);
unique_ptr<Tuna> copyTuna;
copyTuna = myTuna;
```

# 第 27 节

### 使用流进行输入和输出

实际上你在整本书中一直在使用流，从第 1 节“入门”开始，在该节中使用 `std::cout` 在屏幕上显示了“Hello World”。现在是给 C++ 的这部分应关注，并从实用的角度学习流了。在本节中，你将了解到：

- 什么是流以及如何使用
- 如何使用流读写文件
- 有用的 C++ 流操作

## 流的概念
