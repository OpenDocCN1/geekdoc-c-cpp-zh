
```
28: {
29:     cout << "Copy constructor: copying from MyString" << endl;
30:
31:     if(CopySource.Buffer != NULL)
32:     {
33:         // 通过分配缓冲区进行深拷贝
34:             Buffer = new char[strlen(CopySource.Buffer) + 1];
35:
36:         // 从源拷贝到本地缓冲区
37:             strcpy(Buffer, CopySource.Buffer);
38:
39:         // 显示本地缓冲区指向的内存地址
40:             cout << "Buffer points to: 0x" << hex;
41:             cout << (unsigned int*)Buffer << endl;
42:
43:     }
44:     else
45:         Buffer = NULL;
46:     }
47:
48:     // 析构函数
49:     ~MyString()
50:     {
51:         cout << "Invoking destructor, clearing up " << endl;
52:         if (Buffer != NULL)
53:             delete [] Buffer;
54:     }
55:
56:     int GetLength()
57:     {
58:         return strlen(Buffer);
59:     }
60:
61:     const char* GetString()
62:     {
63:         return Buffer;
64:     }
65:
66:     void UseMyString(MyString Input)
67:     {
68:         cout << "String buffer is " << Input.GetLength() << " characters";
69:         cout << " contains: " << Input.GetString() << endl;
70:     }
71:
72:     return;
73: }
74:
75: int main()
76: {
77:     MyString SayHello("Hello from String");
78:     UseMyString(SayHello);
79:     return 0;
80: }
```

### 输出

```
Constructor: creating new MyString
Buffer points to: 0x...
Copy constructor: copying from MyString
Buffer points to: 0x...
String buffer is 17 characters contains: Hello from String
Invoking destructor, clearing up 
Invoking destructor, clearing up 
```

# 警告

在拷贝构造函数的声明中使用 `const` 可以确保拷贝构造函数不会修改所引用的源对象。

此外，拷贝构造函数中的参数是通过引用传递的。如果这一个引用，构造函数本身将通过值进行拷贝，导致源数据发生浅拷贝——这恰恰是你想要规避免的。

| 应该 (DO) | 不应该 (DON'T) |
| :--- | :--- |
| 当你的类包含原始指针成员（`char*` 等）时，务必编写拷贝构造函数和拷贝赋值运算符。 | 除非绝对避免，否则不要使用原始指针作为类成员。 |
| 始终编写带有 `const` 引用源参数的拷贝构造函数。 |  |
| 始终使用如 `std::string` 等字符串类和智能指针类作为成员，而不是原始指针，因为它们实现了拷贝构造函数并节省了你的精力。 |  |

### 注意

带有原始指针成员 `char* Buffer` 的 `MyString` 类被用作示例，以解释拷贝构造函数的必要性。

如果你编写一个需要包含名称等字符串数据的类，你将使用 `std::string` 代替 `char*`，在没有原始指针的情况下，可能甚至不需要拷贝构造函数。这是因为编译器插入的默认拷贝构造函数会确保调用成员对象（如 `std::string`）的所有可用拷贝构造函数。

## C++11

# 移动构造有助于提高性能

由于语言的性质及其需求，某些对象会自动执行拷贝步骤。考虑以下情况：

```cpp
class MyString
```

# 第 9 Lesson：类与对象

```cpp
// 采用列表 9.9 中的实现
MyString Copy(MyString& Source)
{
    MyString CopyForReturn(Source.GetString()); // 创建拷贝
    return CopyForReturn; // 返回值触发拷贝构造函数
}
int main()
{
    MyString sayHello("Hello World of C++");
    MyString sayHelloAgain(Copy(sayHello)); // 调用了 2 次拷贝构造函数

    return 0;
}
```

如所示，在实例化 `sayHelloAgain` 时，拷贝构造函数被调用了两次，由于我们调用了返回 `MyString` 值的函数 `Copy(sayHello)`，因此执行了深拷贝。然而，这个返回的值是临时的，在表达式表达式外部不可用。因此，C++ 编译器诚实调用的拷贝构造函数会导致性能下降，如果它是一个包含大型对象的动态数组，这种下降可能会变得显著。

为了避免这个瓶颈，除了拷贝构造函数外，再编写一个移动构造函数。移动构造函数的语法如下：

```cpp
// 移动构造函数
MyString(MyString&& Buffer : NULL)
{
    if(MoveSource.Buffer)
    {
        Buffer = MoveSource.Buffer; // 获取所有权，即“移动”
        MoveSource.Buffer = NULL; // 将移动源设为 NULL，即释放它
    }
}
```

（注：此处代码逻辑演示）

在可用时，C++11 编译器会自动选择移动构造函数来“移动”临时资源并避免深拷贝步骤。在实现移动构造函数后，注释应适当更改为如下：

```cpp
MyString sayHelloAgain(Copy(sayHello)); // 调用 1 次拷贝构造函数，1 次移动构造函数
```

移动构造函数通常与移动赋值运算符一起实现，将在第 12 Lesson 中进行更详细的讨论。12.11 是实现了移动构造函数和移动赋值运算符的 `MyString` 类更好的版本。

# 构造函数和析构函数的不同用途

在本节中你学习了一些重要且基础的概念，例如构造函数、析构函数的概念，以及通过 `public` 和 `private` 等关键字对数据和方法进行抽象。这些概念使你能够创建控制其如何被创建、拷贝、销毁或暴露数据的类。

让我们来看一些有助于你解决许多重要设计问题的有趣模式。

# 不允许拷贝的类

你被要求为你国家的宪法建模。一个国家只有一个总统。你的 `President` 类面临以下风险：

```cpp
President OurPresident;
DoSomething(OurPresident); // 按值传递时的重复创建
President clone;
clone = OurPresident; // 通过赋值产生重复
```

显然，你需要避免这种情况。通过对特定宪法建模，你可能正在编写一个操作系统并建模一个局域网、一个处理器等。你需要避免资源可以被拷贝的情况。如果你不声明拷贝构造函数，C++ 编译器为你插入一个默认的公有拷贝构造函数。这破坏了你的设计并威胁了你的实现。然而，语言给了你一个这种设计范式的解决方案。

你可以通过声明私有的拷贝构造函数来确保你的类不能被拷贝。这确保了函数调用 `DoSomething(OurPresident)` 将导致编译失败。为了避免赋值，你声明了一个私有的赋值运算符。

因此，解决方案如下：

```cpp
class President
{
private:
    President(const President&); // 私有拷贝构造函数
    President& operator=(const President&); // 私有拷贝赋值运算符

    // - 其他属性
};
```

不需要实现私有的拷贝构造函数或赋值运算符。将它们声明为私有已经足以实现你确保 `President` 类对象不可拷贝的目标。

# 允许单个实例的单例类

之前讨论的 `President` 类很好，但它有一个缺点：它无法帮助通过实例化多个对象来创建多个实例：

`President One, Two, Three;`

得益于私有的拷贝构造函数，它们单独是不可拷贝的，但你理想的是一个类且只有一个真实世界的体现——也就是说，只有一个对象，并且禁止创建额外的对象。

### 提示

| 当 `static` 关键字用于类成员时，该成员在所有实例间共享。 |
| 当 `static` 关键字用于函数作用域内的变量时，它在函数调用之间保留值。 |
| 当 `static` 关键字用于成员方法时，该方法在所有实例间共享。 |

列表 9.10 禁止拷贝、赋值和多次实例化

```cpp
0: #include <iostream>
1: #include <string>
2: using namespace std;
3:
4: class President
5: {
6: private:
7: 私有默认构造函数（禁止外部创建）
8: President() {};
9:
10:     // 私有拷贝构造函数（禁止拷贝创建）
11:     President(const President&);
12:
13:     // 私有赋值运算符（禁止赋值）
14:     const President& operator=(const President&);
15:
16:     // 成员数据：总统的名字
17:     string Name;
18: 
19:     public:
20:     // 控制实例化
21:     static President& GetInstance()
22:     {
23:         // 静态对象只构造一次
24:         static President OnlyInstance;
25: 
26:         return OnlyInstance;
27:     }
28: 
29:     // 公有方法
30:     string GetName()
31:     {
32:         return Name;
33:     }
34: 
35:     void SetName(string InputName)
36:     {
37:         Name = InputName;
38:     }
39:     }
40: 
41: int main()
42: {
43:     President& OnlyPresident = President::GetInstance();
44:     OnlyPresident.SetName("Abraham Lincoln");
45: 
46: 
47:     // 取消注释查看编译失败如何阻止重复
48:     // President Second; // 无法访问构造函数
49:     // President* Third= new President(); // 无法访问构造函数
50:     // President Fourth = OnlyPresident; // 无法访问拷贝构造函数
51:     // OnlyPresident = President::GetInstance(); // 无法访问 operator=
52: 
53:     cout << "The name of the President is: ";
54:     cout << President::GetInstance().GetName() << endl;
55:     return 0;
56: }
```

### 输出

总统的名字是：Abraham Lincoln

### 分析

快速查看一下 `main()` 函数，它包含几行代码和大量的注释行，这些注释展示了在创建 `President` 类的新实例或副本时所有无法运行的组合。让我们逐行分析它们：

+ 47: // President Second; // 无法访问构造函数

48: // President* Third= new President(); // 无法访问构造函数

第 47 行和第 48 行分别通过默认构造函数在栈和堆上创建对象，但由于该构造函数是私有的，因此它是不可用的，如第 8 行所示：

+ 49: // President Fourth = OnlyPresident(); // 无法访问拷贝构造函数

第 49 行试图通过拷贝构造函数对现有对象的拷贝（在创建时进行赋值会调用拷贝构造函数），这在 `main()` 中是不可用的，因为它在第 11 行被声明为私有。

+ 50: // OnlyPresident = President::GetInstance(); // 无法访问 operator=

第 50 行正尝试通过赋值进行拷贝，这是行不通的，因为赋值操作在第 14 行被声明为私有。因此，`main()` 永远无法创建 `President` 类的实例，唯一的选择是第 43 行，那里它使用了静态函数 `GetInstance()`。这是一个静态成员，它非常像全局函数，不需要对象作为句柄即可被调用。在第 21-27 行实现的 `GetInstance()` 使用静态变量来确保 `President` 类只有一个且只有一个实例。为了理解这一点，第 24 行只执行一次（静态初始化），因此 `GetInstance()` 返回 `President` 类的唯一可用实例，无论该实例被如何使用，如 `main()` 中的第 43 行和第 53 行所示。

# 注意事项

考虑到应用程序及其功能的未来增长，请仅在绝对必要时使用单例模式（singleton pattern）。请注意，这种限制多个实例创建的特性本身，当出现需要该类的多个实例的使用场景时，可能会成为架构上的瓶颈。

例如，如果我们的项目正在从建模国家增长到建模联合国（目前由 192 个国家和 192 位总统组成），显然我们正面临着即将酿成的架构问题。

# 禁止在栈上实例化的类

栈空间通常是有限的。如果你正在编写一个内部结构可能包含 GB 级数据的，你可能希望确保该类的客户端不能在它的栈上实例化；相反，它被强制在堆上创建实例。确保此点的关键是将析构函数声明为私：

```cpp
class MonsterDB
{
private:
    // 私有析构
    ~MonsterDB();
    // 预留大量数据的集合
};
```

因此，当尝试使用类 `MonsterDB` 时，不允许创建如下实例：

```cpp
int main()
{
    MonsterDB myDatabase; // 编译错误
    // 更多代码
    return 0;
}
```

这个实例如果成功构建，将位于栈上。然而，由于编译器知道 `myDatabase` 在离开作用域时需要销毁，会自动尝试在 `main()` 结束时调用析构函数，但由于它是私有的，无法访问，导致编译失败。

但是，私有析构函数并阻止你在堆上实例化：

```cpp
int main()
{
    MonsterDB* myDatabase = new MonsterDB(); // 无错误
    // 更多代码
    return 0;
}
```

如果你在那里看到了内存泄漏，你并没有看错。由于无法从 `main` 访问，你也无法删除它。`MonsterDB` 类需要支持的是一个静态公共成员函数来销毁实例（作为成员，它可以访问析构函数）。请参阅列表 9.11。

# 列表 9.11 一个仅允许在自由存储器（使用 new）上创建对象的数据库类 MonsterDB

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class MonsterDB
4: {
5: private:
6:   ~MonsterDB() {}; // 私有析构
7:
8: public:
9:   static void DestroyInstance(MonsterDB* pInstance)
10:  {
11:    // 静态成员可以访问私有析构
12:    delete pInstance;
13:  }
14:
15:  // ... 想象还有其他几个方法
16: };
17:
18: int main()
19: {
20:   MonsterDB* pMyDatabase = new MonsterDB();
21:
22:   // pMyDatabase -> 成员方法 (....)
23:
24:   // 取消下一行的注释以查看编译失败
25:   delete pMyDatabase; // 私有析构无法被调用
26:
27:   // 使用静态成员释放内存
28:   MonsterDB::DestroyInstance(pMyDatabase);
29:
30:   return 0;
31: }
```

### 分析

代码目的是演示如何通过私有析构函数（如第 6 行所示）和静态函数 `DestroyInstance()`（如第 9-13 行所示，在第 28 行的 `main()` 中使用）编写一个禁止在栈上创建的类。
