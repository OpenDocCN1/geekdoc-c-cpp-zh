

这个内存泄漏有点更微妙，但仍然存在泄漏。函数体中的第一行，`int* drip2 = new int(50);`，在堆上分配一块新内存，将 50 赋给它，并让 `drip2` 指向那块内存。到目前为止，一切都很好。第二行，`drip2 = new int(100);`，让 `drip2` 指向堆上的另一块新内存，其中存储 100。问题是，堆上存储 50 的内存现在没有任何指针指向它，因此程序无法释放该内存。因此，该块内存基本上已从系统中泄漏出去。请查看图 9.5，了解泄漏发生的视觉表示。

![](img/34f09be0ed6217c465debc4490197d4f_325_0.png)

**Figure 9.5** By changing `drip2` so that it points to the memory that stores 100, the memory that stores 50 is no longer accessible and has leaked out of the system.

函数的最后一条语句，`delete drip2;`，释放存储 100 的内存，因此这不会成为另一个内存泄漏的来源。但请记住，堆上存储 50 的内存仍然已从系统中泄漏出去。此外，我不担心 `drip2`，它在技术上已成为一个悬空指针，因为它将在函数结束时不复存在。

## Working with Data Members and the Heap

你已经看到如何使用聚合来声明存储对象的成员数据，但你也可以声明指向堆上值的指针成员数据成员。你可能会出于与在其他情况下使用指针相同的一些原因使用指向堆上值的成员数据。例如，你可能想要为一个大型 3D 场景声明一个数据成员；然而，你可能只能通过指针访问 3D 场景。不幸的是，当你使用指向堆上值的成员数据时，由于某些默认对象行为的工作方式，可能会出现问题。但你可以通过编写成员函数来改变这些默认行为，从而避免这些问题。

### Introducing the Heap Data Member Program

堆数据成员程序定义了一种新型的 critter，其数据成员是指针，指向存储在堆上的对象。类定义了一些新的成员函数来处理对象被销毁、复制或分配给另一个对象的情况。程序销毁、复制和分配对象，以显示即使数据成员指向堆上的值，对象的行为也符合预期。图 9.6 显示了堆数据成员程序的结果。

![](img/34f09be0ed6217c465debc4490197d4f_326_0.png)

**Figure 9.6** Objects, each with a data member that points to a value on the heap, are instantiated, destroyed, and copied.

你可以从 Course Technology 网站 (www.courseptr.com/downloads) 下载此程序的代码。该程序位于第 9 章文件夹中；文件名是 `heap_data_member.cpp`。

```cpp
//Heap Data Member

//Demonstrates an object with a dynamically allocated data member

#include <iostream>

#include <string>

using namespace std;

class Critter

{

public:

    Critter(const string& name = "", int age = 0);

    ~Critter();                        //destructor prototype

    Critter(const Critter& c);         //copy constructor prototype

    Critter& operator=(const Critter& c);  //overloaded assignment op

    void Greet() const;

private:

    string* m_pName;

    int m_Age;

};

Critter::Critter(const string& name, int age)

{

    cout << "Constructor called\n";

    m_pName = new string(name);

    m_Age = age;

}

Critter::~Critter()                     // destructor definition

{

    cout << "Destructor called\n";

    delete m_pName;

}

Critter::Critter(const Critter& c)      // copy constructor definition

{

    cout << "Copy Constructor called\n";

    m_pName = new string(*(c.m_pName));

    m_Age = c.m_Age;

}

Critter& Critter::operator=(const Critter& c)  // overloaded assignment op definition

{

    cout << "Overloaded Assignment Operator called\n";

    if (this != &c)

    {

        delete m_pName;

        m_pName = new string(*(c.m_pName));

        m_Age = c.m_Age;

    }

    return *this;

}

void Critter::Greet() const

{

    cout << "I'm " << *m_pName << " and I'm " << m_Age << " years old.\n";

    cout << "&m_pName: " << &m_pName << endl;

}

void testDestructor();

void testCopyConstructor(Critter aCopy);

void testAssignmentOp();

int main()

{

    testDestructor();

    cout << endl;

    Critter crit("Poochie", 5);

    crit.Greet();

    testCopyConstructor(crit);

    crit.Greet();

    cout << endl;

    testAssignmentOp();

    return 0;

}

void testDestructor()

{

    Critter toDestroy("Rover", 3);

    toDestroy.Greet();

}

void testCopyConstructor(Critter aCopy)

{

    aCopy.Greet();

}

void testAssignmentOp()

{

    Critter crit1("crit1", 7);

    Critter crit2("crit2", 9);

    crit1 = crit2;

    crit1.Greet();

    crit2.Greet();

    cout << endl;

    Critter crit3("crit", 11);

    crit3 = crit3;

    crit3.Greet();

}

```

### Declaring Data Members that Point to Values on the Heap

要声明指向堆上值的成员数据，首先需要声明一个指向指针的成员数据。这正是我在 Critter 中所做的，下面这一行将 `m_pName` 声明为指向字符串对象的指针。

```cpp
string* m_pName;
```

在类构造函数中，你可以在堆上分配内存，为内存分配一个值，然后让指针数据成员指向该内存。这正是我在构造函数定义中所做的，下面这一行为字符串对象分配内存，将 `name` 赋给它，并让 `m_pName` 指向堆上的那块内存。

```cpp
m_pName = new string(name);
```

我还声明了一个不是指针的数据成员：

```cpp
int m_Age;
```

这个数据成员在构造函数中以你之前见过的方式获取其值，使用简单的赋值语句：

```cpp
m_Age = age;
```

你将看到这些数据成员在 Critter 对象被销毁、复制和相互赋值时是如何被不同对待的。

现在，第一个具有堆上数据成员的对象是在 `main()` 调用 `testDestructor()` 时创建的。对象 `toDestroy` 具有一个 `m_pName` 数据成员，指向存储在堆上等于 `"Rover"` 的字符串对象。图 9.7 提供了 Critter 对象的视觉表示。请注意，该图像是抽象的，因为 critter 的名称实际上存储为字符串对象，而不是字符串文字。

![](img/34f09be0ed6217c465debc4490197d4f_330_0.png)

**Figure 9.7** A representation of a Critter object. The string object equal to `"Rover"` is stored on the heap.

### Declaring and Defining Destructors

当对象的成员数据指向堆上的值时，可能会出现的一个问题是内存泄漏。这是因为当对象被删除时，指向堆值的指针会随之消失。如果堆值仍然存在，就会产生内存泄漏。为了避免内存泄漏，对象应在被销毁前自行清理，删除其关联的堆值。幸运的是，有一个成员函数，析构函数，在对象被销毁前被调用，可用于执行必要的清理。

如果不编写自己的析构函数，编译器为你创建的默认析构函数不会尝试释放数据成员可能指向的堆上的任何内存。这种行为对于简单的类通常是可以的，但当你有一个类，其数据成员指向堆上的值时，你应该编写自己的析构函数，以便在对象消失前释放与对象关联的堆上的内存，从而避免内存泄漏。这正是我在 Critter 类中所做的。首先，在类定义内部，我声明了析构函数。请注意，析构函数以类的名称开头，后跟 `~`（波浪号字符），并且没有参数也不返回值。

```cpp
Critter::~Critter()                 //destructor definition

{

    cout << "Destructor called\n";

    delete m_pName;

}

```

在 `main()` 中，我在调用 `testDestructor()` 时对析构函数进行了测试。该函数创建一个 Critter 对象 `toDestroy`，并调用其 `Greet()` 方法，该方法显示 `I’m Rover and I’m 3 years old. &m_pName: 73F2ED48003AF644`。该消息提供了一种查看对象 `m_Age` 数据成员的值和其 `m_pName` 数据成员指向的字符串的方法。但它也显示了指针 `m_pName` 中存储的堆上字符串的地址。重要的是要注意的是，在显示完 `Greet()` 消息后，函数结束，`toDestroy` 就可以被销毁了。幸运的是，在发生这种情况之前，`toDestroy` 的析构函数会自动被调用。析构函数会显示 `Destructor called` 并删除堆上等于 `"Rover"` 的字符串对象，在清理自身的同时不会泄漏内存。析构函数不会对 `m_Age` 数据成员做任何事。这完全没问题，因为 `m_Age` 不在堆上，而是 `toDestroy` 的一部分，会和 Critter 对象的其余部分一起被正确释放。

### Hint

当你有一个在堆上分配内存的类时，你应该编写一个析构函数来清理并释放该内存。

## Declaring and Defining Copy Constructors

有时对象会被自动复制给你。这发生在对象：

- 按值传递给函数
- 从函数返回
- 通过初始化器初始化为另一个对象
- 作为对象构造函数的单个参数提供

复制工作由一个特殊的成员函数完成，称为拷贝构造函数。与构造函数和析构函数一样，如果你不自己编写，默认的拷贝构造函数会为你提供。默认的拷贝构造函数只是将每个数据成员的值复制到新对象中同名的数据成员——逐成员复制。

对于简单的类，默认的拷贝构造函数通常就足够了。然而，当你有一个类，其数据成员指向堆上的值时，你应该考虑编写自己的拷贝构造函数。为什么？想象一个 Critter 对象，它有一个数据成员是指向堆上字符串对象的指针。仅使用默认拷贝构造函数，对象的自动复制会产生一个新对象，该对象指向堆上同一个字符串，因为新对象的指针只是简单地获得了原始对象指针中存储的地址的副本。这种逐成员复制会产生浅拷贝，其中副本的指针数据成员指向与原始对象指针数据成员相同的内存块。

让我给你一个具体的例子。如果我没有在 Heap Data Member 程序中编写自己的拷贝构造函数，当我通过以下函数调用按值传递一个 Critter 对象时，程序会自动对 `crit` 进行浅拷贝，名为 `aCopy`，在 `testCopyConstructor()` 中存在。

```cpp
testCopyConstructor(crit);
```

`aCopy` 的 `m_pName` 数据成员将指向与 `crit` 的 `m_pName` 数据成员完全相同的堆上字符串对象。图 9.8 显示了我的意思。请注意，该图像是抽象的，因为生物的名字实际上存储为字符串对象，而不是字符串字面量。

![](img/34f09be0ed6217c465debc4490197d4f_332_0.png)

**Figure 9.8** 如果对 `crit` 进行浅拷贝，`aCopy` 和 `crit` 将各有一个数据成员指向堆上的同一块内存。

为什么这是个问题？一旦 `testCopyConstructor()` 结束，`aCopy` 的析构函数就会被调用，释放 `aCopy` 的 `m_pName` 数据成员指向的堆内存。因此，`crit` 的 `m_pName` 数据成员将指向已被释放的内存，这意味着 `crit` 的 `m_pName` 数据成员将成为悬空指针！图 9.9 为你提供了此情况的视觉表示。请注意，该图像是抽象的，因为生物的名字实际上存储为字符串对象，而不是字符串字面量。

你真正需要的是一个拷贝构造函数，它为每个指向堆对象的指针数据成员产生一个新对象，并在堆上为其分配自己的内存块——深拷贝。这就是我在为类定义拷贝构造函数时所做的，它取代了编译器提供的默认拷贝构造函数。首先，在类定义内部，我声明拷贝构造函数：

```cpp
Critter(const Critter& c);    //copy constructor prototype
```

接下来，在类定义外部，我定义拷贝构造函数：

```cpp
Critter::Critter(const Critter& c)    //copy constructor definition

{

    cout << "Copy Constructor called\n";

    m_pName = new string(*(c.m_pName));

    m_Age = c.m_Age;

}

```

![](img/34f09be0ed6217c465debc4490197d4f_333_0.png)

**Figure 9.9** 如果浅拷贝的 Critter 对象被销毁，它与原始对象共享的堆内存将被释放。结果，原始对象将拥有一个悬空指针。

