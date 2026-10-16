

Q: 何时应使用友元函数？

A: 当你需要一个函数能够访问类的非公有成员时。

Q: 什么是友元成员函数？

A: 一个可以访问另一个类所有成员的类的成员函数。

Q: 什么是友元类？

A: 一个可以访问另一个类所有成员的类。

Q: 运算符重载会不会变得令人困惑？

A: 会的。给运算符赋予过多含义或不直观的含义会导致代码难以理解。

Q: 当我在堆上实例化一个新对象时会发生什么？

A: 所有的数据成员都将占用堆上的内存而不是栈上。

Q: 我能否通过一个常量指针访问对象？

A: 可以。但你只能通过常量指针访问常量成员函数。

Q: 浅拷贝有什么问题？

A: 因为浅拷贝共享对同一块内存的引用，对一个对象的更改会反映在另一个对象中。

Q: 什么是链表？

A: 一种由一系列链接节点组成的有序动态数据结构。

Q: 链表与向量有何不同？

A: 链表允许在列表的任何位置插入和删除节点，但不允许像向量那样的随机访问。然而，在链表中间插入和删除节点可能比在向量中间插入和删除元素更高效。

Q: STL 中是否有一种容器类用作链表？

A: 有，list 类。

Q: 游戏大厅程序中使用的数据结构是链表吗？

A: 它与链表相似，但实际上是一个队列。

Q: 什么是队列？

A: 一种元素按进入顺序被移除的数据结构。此过程通常称为先进先出（FIFO）。

Q: STL 中是否有一种容器可用作队列？

A: 有，queue 容器适配器。

### Discussion Questions

1. 你可以用聚合创建哪些类型的游戏实体？
2. 友元函数是否破坏了 OOP 中的封装？
3. 动态内存为游戏程序提供了哪些优势？
4. 为什么内存泄漏难以追踪？
5. 是否应始终要求在堆上分配内存的对象释放它？

### Exercises

1. 通过编写 Player 类的友元函数来改进游戏大厅程序中的 Lobby 类，该函数允许 Player 对象被发送到 cout。接下来，更新允许 Lobby 对象被发送到 cout 的函数，使其使用你的新函数来发送 Player 对象到 cout。

2. 游戏大厅程序中的 Lobby::AddPlayer() 成员函数效率低下，因为它遍历所有玩家节点以将新玩家添加到队伍末尾。向 Lobby 类添加一个 m_pTail 指针数据成员，该成员始终指向队伍中最后一个玩家节点，并使用它更高效地添加玩家。

3. 以下代码有什么问题？

```
#include <iostream>
using namespace std;

int main()
{
    int* pScore = new int;
    *pScore = 500;
    pScore = new int(1000);
    delete pScore;
    pScore = 0;

    return 0;
}
```

## CHAPTER 10 INHERITANCE AND POLYMORPHISM: BLACKJACK

![](img/34f09be0ed6217c465debc4490197d4f_353_0.png)

类为你提供了表示具有属性和行为的游戏实体的完美方式。但游戏实体通常是相关的。在本章中，你将学习继承和多态，它们为你提供了表达这些联系的方式，并且可以使定义和使用类变得更简单、更直观。具体来说，你将学习：

- 从另一个类派生一个类
- 使用继承的数据成员和成员函数
- 重写基类成员函数
- 定义虚函数以实现多态
- 声明纯虚函数以定义抽象类

### INTRODUCING INHERITANCE

OOP 的关键要素之一是 *继承*，它允许你从现有类 *派生* 新类。这样做时，新类会自动 *继承*（或获得）现有类的数据成员和成员函数。就像免费获得了现有类所做的开发工作一样！

继承在你想要创建现有类的更专业版本时尤其有用，因为你可以向新类添加数据成员和成员函数来扩展它。例如，想象你有一个类 Enemy，它定义了游戏中一个敌人，具有成员函数 Attack() 和数据成员 `m_Damage`。你可以从 `Enemy` 派生一个新类 `Boss` 用于 Boss。这意味着 `Boss` 可以自动拥有 `Attack()` 和 `m_Damage`，而无需你为它们编写任何代码。然后，为了让 Boss 更难对付，你可以在 `Boss` 类中添加成员函数 `SpecialAttack()` 和数据成员 `DamageMultiplier`。请看图 10.1，它展示了 `Enemy` 和 `Boss` 类之间的关系。

![](img/34f09be0ed6217c465debc4490197d4f_354_0.png)

图 10.1
`Boss` 从 `Enemy` 继承 `Attack()` 和 `m_Damage`，同时定义 `SpecialAttack()` 和 `m_DamageMultiplier`。

继承的众多优势之一是你可以重用已经编写的类。这种可重用性带来的好处包括：

- **更少的工作。** 无需重新定义你已有的功能。一旦你有一个为其他类提供基础功能的类，就不必再次编写该代码。
- **更少错误。** 一旦你有一个无 bug 的类，你可以重用它而不会在其中出现错误。
- **更清晰的代码。** 因为基类的功能在程序中只存在一次，你不必反复浏览相同的代码，这使得程序更容易理解和修改。

大多数相关的游戏实体都呼唤使用继承。无论是玩家面对的一系列敌人，玩家指挥的军事车辆中队，还是玩家使用的武器库存，你都可以使用继承来以彼此为基准定义这些游戏实体组，从而实现更快、更轻松的编程。

### Introducing the Simple Boss Program

Simple Boss 程序演示了继承。在其中，我定义了一个低级敌人的类 Enemy。从这个类，我派生了一个新的类 Boss，用于玩家必须面对的强力 Boss。然后，我实例化一个 Enemy 对象并调用其 Attack() 成员函数。接下来，我实例化一个 Boss 对象。我能够为 Boss 对象调用 Attack()，因为它从 Enemy 继承了该成员函数。最后，我调用 Boss 对象的 SpecialAttack() 成员函数，这是我在 Boss 中定义的特殊攻击。由于我在 Boss 中定义了 SpecialAttack()，只有 Boss 对象可以使用它。Enemy 对象没有这种特殊攻击。图 10.2 显示了程序的结果。

![](img/34f09be0ed6217c465debc4490197d4f_355_0.png)

图 10.2
Boss 类继承 Attack() 成员函数，然后定义自己的 SpecialAttack() 成员函数。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载此程序的代码。该程序位于第 10 章文件夹中；文件名是 simple_boss.cpp。

```
//Simple Boss
//Demonstrates inheritance

#include <iostream>
using namespace std;

class Enemy
{
public:
    int m_Damage;

    Enemy();
    void Attack() const;
};

Enemy::Enemy():
    m_Damage(10)
{}

void Enemy::Attack() const
{
    cout << "Attack inflicts " << m_Damage << " damage points!\n";
}

class Boss : public Enemy
{
public:
    int m_DamageMultiplier;

    Boss();
    void SpecialAttack() const;
};
Boss::Boss():
    m_DamageMultiplier(3)
{}

void Boss::SpecialAttack() const
{
    cout << "Special Attack inflicts " << (m_DamageMultiplier * m_Damage);
    cout << " damage points!\n";
}

int main()
{
    cout << "Creating an enemy.\n";
    Enemy enemy1;
    enemy1.Attack();

    cout << "\nCreating a boss.\n";
    Boss boss1;
    boss1.Attack();
    boss1.SpecialAttack();

    return 0;
}
```

### Deriving from a Base Class

当我用以下行定义 Boss 时，我从 Enemy 派生 Boss 类：

```
class Boss : public Enemy
```

Boss 基于 Enemy。事实上，Enemy 被称为基类（或超类），而 Boss 是派生类（或子类）。这意味着 Boss 继承 Enemy 的数据成员和成员函数，受访问控制限制。在这种情况下，Boss 继承并可以直接访问 m_Damage 和 Attack()。就好像我在 Boss 中同时定义了 m_Damage 和 Attack() 一样。

### Hint

你可能已经注意到，我将类的所有成员都设为 public，包括其数据成员。我这样做是因为它使基类和派生类的最简单第一个示例更简单。你可能还注意到我在从 Enemy 派生 Boss 时使用了关键字 public。现在不要担心这个问题。我将在下一个示例程序 Simple Boss 2.0 中全部介绍。

