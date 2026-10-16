

在 main() 中，我调用了一个函数来测试该类的重载赋值运算符。

```
testAssignmentOp();
```

testAssignmentOp() 创建了两个对象并将一个赋给另一个。

```
Critter crit1("crit1", 7);
Critter crit2("crit2", 9);
crit1 = crit2;
```

前面的赋值语句，crit1 = crit2;，调用了 crit1 的赋值运算符成员函数——operator=()——。在 operator=() 函数中，c 是指向 crit2 的常量引用。该成员函数的目标是将 crit2 的所有数据成员的值赋给 crit1，同时确保每个 Critter 对象对任何指针数据成员都有自己在堆上的内存块。

在 operator=() 显示出重载的赋值运算符已被调用后，它使用了 this 指针。什么是 this 指针？它是所有非静态成员函数自动拥有的一个指针，指向用于调用该函数的对象。在这种情况下，this 指向 crit1，即被赋值的对象。

下一行，if (this != &c)，检查 crit1 的地址是否不等于 crit2 的地址——也就是说，它测试对象是否未被自身赋值。因为不是，所以与 if 语句关联的代码块被执行。

在 if 块内部，delete m_pName; 释放了堆上 crit1 的 m_pName 数据成员所指向的内存。行 m_pName = new string(*(c.m_pName)); 在堆上分配一个新的内存块，获取 crit2 的 m_pName 数据成员所指向的字符串的副本，将字符串对象复制到新的堆内存中，并使 crit1 的 m_pName 数据成员指向此内存。你应该对所有指向堆上内存的数据成员遵循此逻辑。

块中的最后一行，m_Age = c.m_Age; 只是简单地将 crit2 的 m_Age 值复制到 crit1 的 m_Age 数据成员。你应该对所有不是指向堆上内存的指针的数据成员遵循这种简单的逐成员复制。

最后，成员函数通过返回 *this 返回新 crit1 的副本。你应该对你编写的任何重载赋值运算符成员函数做同样的处理。

回到 testAssignmentOp() 中，我通过调用 crit1.Greet() 和 crit2.Greet() 来证明赋值是成功的。crit1 显示的消息是 I'm crit2 and I'm 9 years old. &m_pName: 73F2ED48003AF644 而 crit2 显示的消息是 I'm crit2 and I'm 9 years old. &m_pName: 73F2ED48003AF634。每个消息的第一部分，I'm crit2 and I'm 9 years old.，是相同的，表明值的复制是成功的。每个消息的第二部分是不同的，表明每个对象指向堆上的不同内存块，这证明我在赋值后避免了浅拷贝，并且拥有真正独立的对象。

在对重载赋值运算符的最后一次测试中，我演示了将对象自身赋给自身时会发生什么。接下来在函数中我就是这样做的，使用以下行：

```
Critter crit3("crit", 11);
crit3 = crit3;
```

前面的赋值语句，crit3 = crit3;，调用了 crit3 的赋值运算符成员函数——operator=()——。if 语句检查 crit3 是否被自身赋值。因为是，所以成员函数只是通过 return *this 返回对该对象的引用。你应该在自己的重载赋值运算符中遵循此逻辑，因为在赋值中只有一个对象参与时可能会出现潜在问题。

## Hint

当你有一个类，其数据成员指向堆上的内存时，你应该考虑为该类重载赋值运算符。

## INTRODUCING THE GAME LOBBY PROGRAM

游戏大厅程序模拟了一个游戏大厅——通常在在线游戏中，玩家等待的区域。该程序实际上并不涉及在线组件。它创建了一条玩家可以等待的单一队列。程序的用户运行模拟并有四个选择。他可以向大厅添加一个人，从大厅中移除一个人（队列中的第一个人最先离开），清空大厅，或退出模拟。图 9.11 显示了程序的运行情况。

![](img/34f09be0ed6217c465debc4490197d4f_338_0.png)

## Figure 9.11

大厅容纳的玩家按加入的顺序被移除。

## The Player Class

我做的第一件事是创建一个 Player 类来表示在大厅中等待的玩家。因为我不知道大厅中一次会有多少玩家，所以使用动态数据结构是有意义的。通常，我会去我的工具箱中使用 STL 中的容器。但我决定在该程序中采取不同的方法，并使用我管理的动态分配内存创建自己的容器。我这样做并不是因为这是一个更好的编程选择——总是要看看你是否能利用其他程序员做的好工作，比如 STL——而是因为它能成为一个更好的游戏编程示例。这是一个真正看到动态内存运行的好方法。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载此程序的代码。该程序位于第 9 章文件夹中；文件名是 game_lobby.cpp。以下是程序的开头，其中包含 Player 类：

```
//Game Lobby
//Simulates a game lobby where players wait

#include <iostream>
```

```
#include <string>

using namespace std;

class Player
{
public:
    Player(const string& name = "");
    string GetName() const;
    Player* GetNext() const;
    void SetNext(Player* next);

private:
    string m_Name;
    Player* m_pNext;    //Pointer to next player in list
};

Player::Player(const string& name):
    m_Name(name),
    m_pNext(0)
{}

string Player::GetName() const
{
    return m_Name;
}

Player* Player::GetNext() const
{
    return m_pNext;
}

void Player::SetNext(Player* next)
{
    m_pNext = next;
}
```

m_Name 数据成员保存玩家的名字。这很直接，但你可能对另一个数据成员 m_pNext 有疑问。它是指向 Player 对象的指针，这意味着每个 Player 对象可以保存一个名字并指向另一个 Player 对象。当我谈到 Lobby 类时，你会明白其中的要点

![](img/34f09be0ed6217c465debc4490197d4f_340_0.png)

## Figure 9.12

Player 对象可以保存一个名字并指向另一个 Player 对象。

该类对 m_Name 有一个 get 访问器方法，对 m_pNext 有 get 和 set 访问器成员函数。最后，构造函数很简单。它根据传递给构造函数的参数将 m_Name 初始化为字符串对象。它还将 m_pNext 设置为 0，使其成为空指针。

## The Lobby Class

Lobby 类表示玩家等待的大厅或队列。以下是类的定义：

```
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

数据成员 m_pHead 是一个指向 Player 对象的指针，表示队列中的第一个人。m_pHead 表示队列的头部。

由于每个 Player 对象都有一个 m_pNext 数据成员，你可以将一堆 Player 对象链接成一个链表。链表的各个元素通常

![](img/34f09be0ed6217c465debc4490197d4f_341_0.png)

## Figure 9.13

每个节点保存一个名字和指向列表中下一个玩家的指针。队列中的第一个玩家位于头部。

被称为节点。图 9.13 提供了游戏大厅的视觉表示——一系列玩家节点链接在一起，队列头部有一个玩家。

一种思考玩家节点的方法是将其视为运载货物并连接在一起的火车车厢群。在这种情况下，火车车厢运载名字作为货物，并通过指针数据成员 m_pNext 链接。Lobby 类在堆上为列表中的每个 Player 对象分配内存。Lobby 数据成员 m_pHead 提供对列表头部第一个 Player 对象的访问。

构造函数非常简单。它只是将数据成员 m_pHead 初始化为 0，使其成为空指针。

```
Lobby::Lobby():
    m_pHead(0)
{
```

析构函数只是调用 Clear()，它从列表中移除所有 Player 对象，释放已分配的内存。

```
Lobby::~Lobby()
{
    Clear();
}
```

AddPlayer() 在堆上实例化一个 Player 对象并将其添加到列表末尾。RemovePlayer() 移除列表中的第一个 Player 对象，释放已分配的内存。

我将函数 operator<<( ) 声明为 Lobby 的友元，这样我就可以使用 << 运算符将 Lobby 对象发送到 cout。

