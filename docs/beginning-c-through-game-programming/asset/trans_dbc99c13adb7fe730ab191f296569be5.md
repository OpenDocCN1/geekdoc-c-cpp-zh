

![](img/c7e8651578bccd573227f684823b8754_333_0.png)

图9.9 如果Critter对象的浅拷贝被销毁，它与原对象共享的堆内存将被释放。结果，原对象将拥有一个悬空指针。

这个类替换了编译器提供的默认构造函数。首先，在类定义内部，我声明拷贝构造函数：

```cpp
Critter(const Critter& c);    //copy constructor prototype
```

接下来，在类定义外部，我定义拷贝构造函数：

```cpp
Critter::Critter(const Critter& c)    //copy constructor definition
{
    cout << "Copy Constructor called\n";
    m_pName = new string(*c.m_pName);
    m_Age = c.m_Age;
}
```

就像这个一样，拷贝构造函数必须与类同名。它不返回任何值，但接受对该类对象的引用——也就是需要被拷贝的对象。该引用应作为常量引用，以保护原对象在拷贝过程中不被更改。

拷贝构造函数的工作是将数据成员从原对象复制到拷贝对象。如果原对象的某个数据成员是指向堆中值的指针，则拷贝构造函数应从堆中申请内存，将原始堆值复制到新的内存块中，然后将拷贝对象的相应数据成员指向这块新内存。

当我通过按值传递crit调用testCopyConstructor()时，我编写的拷贝构造函数会被自动调用。从屏幕上出现的文本“Copy Constructor called.”可以看出这一点。我的拷贝构造函数创建了一个新的Critter对象（副本），并在c中接受对原对象的引用。

> 提示
> 当你的类有指向堆内存的数据成员时，应该考虑编写一个拷贝构造函数，为新对象分配内存并创建深拷贝。

## 重载赋值运算符

当赋值语句的两端都是同一个类的对象时，会调用该类的赋值运算符成员函数。与默认拷贝构造函数类似，如果你没有编写自己的赋值运算符，编译器会为你提供一个默认的赋值运算符成员函数。同样，与默认拷贝构造函数一样，默认赋值运算符只提供逐成员复制。

对于简单的类，默认赋值运算符通常足够了。然而，当你的类有一个指向堆中值的数据成员时，应考虑编写自己的重载赋值运算符。如果不这样做，当你将一个对象赋值给另一个对象时，最终会得到对象的浅拷贝。为了避免这个问题，我为Critter重载了赋值运算符。首先，在类定义内部，我写下声明：

```cpp
Critter& Critter::operator=(const Critter& c); //overloaded assignment op
```

接下来，在类定义外部，我写下成员函数定义：

```cpp
Critter& Critter::operator=(const Critter& c)  //overloaded assignment op def
{
    cout << "Overloaded Assignment Operator called\n";
    if (this != &c)
    {
        delete m_pName;
        m_pName = new string(*c.m_pName);
        m_Age = c.m_Age;
    }
    return *this;
}
```

注意，这个成员函数返回对一个Critter对象的引用。为了健壮的赋值操作，请从重载赋值运算符成员函数返回一个引用。

在main()中，我调用了一个测试这个类重载赋值运算符的函数。

```cpp
testAssignmentOp();
```

testAssignmentOp()创建两个对象，并将其中一个赋值给另一个。

```cpp
Critter crit1("crit1", 7);
Critter crit2("crit2", 9);
crit1 = crit2;
```

前面的赋值语句crit1 = crit2会为crit1调用赋值运算符成员函数operator=()。在operator=()函数中，c是对crit2的常量引用。该成员函数的目标是将crit2所有数据成员的值赋给crit1，同时确保每个Critter对象在堆上都有自己的内存块来存放指针数据成员。

在operator=()显示一条消息表明重载赋值运算符已被调用后，它使用了this指针。this指针是什么？它是所有非静态成员函数自动拥有的一个指针，指向用于调用函数的对象。在这个例子中，this指向crit1，即被赋值的对象。

下一行 if (this != &c) 检查crit1的地址是否不等于crit2的地址——也就是说，测试该对象是否没有被赋值给自己。因为确实不是，所以与if语句关联的代码块会执行。

在if代码块内，delete m_pName; 释放crit1的m_pName数据成员所指向的堆内存。m_pName = new string(*c.m_pName); 这一行在堆上分配一块新内存，获取crit2的m_pName数据成员所指向的字符串副本，将字符串对象复制到新的堆内存中，并将crit1的m_pName数据成员指向这块内存。对于所有指向堆内存的数据成员，你都应该遵循这个逻辑。

块中的最后一行 m_Age = c.m_Age; 只是将crit2的m_Age值复制到crit1的m_Age数据成员。对于所有不指向堆内存的数据成员，你应该遵循这种简单的逐成员复制。

最后，成员函数通过返回 *this 返回新crit1的副本。对于你编写的任何重载赋值运算符成员函数，都应该这样做。

回到testAssignmentOp()中，我通过调用crit1.Greet()和crit2.Greet()来证明赋值成功。crit1显示消息 “I'm crit2 and I'm 9 years old. &m_pName: 73F2ED48003AF644”，而crit2显示消息 “I'm crit2 and I'm 9 years old. &m_pName: 73F2ED48003AF634”。每条消息的第一部分 “I'm crit2 and I'm 9 years old.” 相同，表明值复制成功。每条消息的第二部分不同，表明每个对象指向堆上不同的内存块，这证明我避免了浅拷贝，并且在赋值后拥有了真正独立的对象。

在重载赋值运算符的最后一个测试中，我演示了将一个对象赋值给自身时会发生什么。这就是我在函数中接下来要做的，代码如下：

```cpp
Critter crit3("crit", 11);
crit3 = crit3;
```

前面的赋值语句crit3 = crit3; 会为crit3调用赋值运算符成员函数operator=()。if语句会检查crit3是否被赋值给它自己。因为的确如此，成员函数只需通过 return *this; 返回对对象的引用。你应该在自己编写的重载赋值运算符中遵循这个逻辑，因为如果赋值只涉及一个对象，可能会出现潜在问题。

## 提示

> 当你的类有指向堆内存的数据成员时，应考虑为该类重载赋值运算符。

## 游戏大厅程序简介

游戏大厅程序模拟一个游戏大厅——玩家等待的区域，通常出现在在线游戏中。该程序实际上不涉及在线组件。它创建了一条玩家可以等待的单一队列。程序的用户运行模拟，有四个选择：可以将一个人添加到大厅，从大厅移除一个人（队列中的第一个人首先离开），清空大厅，或退出模拟。图9.11展示了程序运行时的样子。

![](img/c7e8651578bccd573227f684823b8754_340_0.png)

图9.12
一个Player对象可以保存一个名称，并指向另一个Player对象。

关于Lobby类。图9.12提供了Player对象的可视化表示。

该类有一个针对m_Name的get访问器方法，以及针对m_pNext的get和set访问器成员函数。最后，构造函数非常简单。它根据传递给构造函数的内容将m_Name初始化为一个字符串对象。它还将m_pNext设置为0，使其成为空指针。

## Lobby类

Lobby类表示玩家等待的大厅或队列。以下是类定义：

```cpp
class Lobby
{
    friend ostream& operator<<(ostream& os, const Lobby& aLobby);

    public:
        Lobby();
        ~Lobby();
        void AddPlayer();
        void RemovePlayer();
        void Clear();

    private:
        Player* m_pHead;
};
```

数据成员m_pHead是一个指向Player对象的指针，该对象表示队列中的第一个人。m_pHead表示队首。

由于每个Player对象都有一个m_pNext数据成员，你可以将许多Player对象链接成一个链表。链表中的单个元素通常

