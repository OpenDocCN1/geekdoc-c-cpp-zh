
```
class Enemy
{
public:
    Enemy(int damage = 10);
    void virtual Taunt() const;      //made virtual to be overridden
    void virtual Attack() const;     //made virtual to be overridden

private:
    int m_Damage;
};

Enemy::Enemy(int damage):
    m_Damage(damage)
{}

void Enemy::Taunt() const
{
    cout << "The enemy says he will fight you.\n";
}

void Enemy::Attack() const
{
    cout << "Attack! Inflicts " << m_Damage << " damage points.";
}

class Boss : public Enemy
{
public:
    Boss(int damage = 30);
    void virtual Taunt() const;      //optional use of keyword virtual
    void virtual Attack() const;     //optional use of keyword virtual
};

Boss::Boss(int damage):
    Enemy(damage)                   //call base class constructor with argument
{}

void Boss::Taunt() const      //override base class member function
{
    cout << "The boss says he will end your pitiful existence.\n";
}
```

## 提示

当你想要向基类构造函数传递特定值时，能够调用它是很有用的。

## 声明虚基类成员函数

任何你期望在派生类中被重写的继承自基类的成员函数，都应该使用关键字 `virtual` 声明为虚函数。当你将一个成员函数声明为 `virtual` 时，你就为成员函数的重写版本提供了一种方式，使其能按预期处理对象的指针和引用。由于我知道我会在派生类 `Boss` 中重写 `Taunt()`，所以我在基类 `Enemy` 中将 `Taunt()` 声明为 `virtual`。

```
void virtual Taunt() const;    //made virtual to be overridden
```

## 陷阱

虽然你可以重写非虚成员函数，但这可能导致你意想不到的行为。一个好的经验法则是，将任何要在派生类中重写的基类成员函数声明为虚函数。

在 `Enemy` 类定义之外，我定义了 `Taunt()`：

```
void Enemy::Taunt() const
{
    cout << "The enemy says he will fight you.\n";
}
```

注意，我没有在定义中使用关键字 `virtual`。你不在成员函数的定义中使用 `virtual`，只在声明中使用。

一旦成员函数被声明为虚函数，它在任何派生类中都是虚函数。这意味着当你重写一个虚成员函数时，不必在声明中使用关键字 `virtual`，但你最好还是使用它，因为它会提醒你该函数确实是虚函数。因此，当我在 `Boss` 中重写 `Taunt()` 时，我明确将其声明为 `virtual`，即使并不是必须的：

```
void virtual Taunt() const;    //optional use of keyword virtual
```

## 重写虚基类成员函数

重写的下一步是在派生类中为成员函数提供一个新的定义。我在 `Boss` 类中就是这样做的：

```
void Boss::Taunt() const    //override base class member function
```

```
{
    cout << "The boss says he will end your pitiful existence.\n";
}
```

当我通过任何 `Boss` 对象调用该成员函数时，这个新定义会被执行。对于所有 `Boss` 对象，它都会替换从 `Enemy` 继承的 `Taunt()` 定义。当我在 `main()` 中使用下面这行代码调用该成员函数时，会显示消息 “The boss says he will end your pitiful existence.”

```
aBoss.Taunt();
```

当你想在派生类中改变或扩展基类成员函数的行为时，重写成员函数是很有用的。

## 陷阱

不要将 override（重写）与 overload（重载）混淆。当你重写一个成员函数时，你在派生类中为其提供一个新的定义。当你重载一个函数时，你创建了具有不同签名的多个版本。

## 陷阱

当你重写一个重载的基类成员函数时，你会隐藏该基类成员函数的所有其他重载版本——这意味着访问该成员函数其他版本的唯一方式是显式调用基类成员函数。因此，如果你重写了一个重载的成员函数，最好重写该重载函数的每一个版本。

## 调用基类成员函数

你可以从派生类的任何函数中直接调用基类成员函数。你所需要做的就是在成员函数名前加上类名和作用域解析运算符。这就是我在为 `Boss` 类定义 `Attack()` 的重写版本时所做的：

```
void Boss::Attack() const     //override base class member function
{
    Enemy::Attack();           //call base class member function
    cout << " And laughs heartily at you.\n";
}
```

代码 `Enemy::Attack();` 显式调用了 `Enemy` 的 `Attack()` 成员函数。由于 `Boss` 中的 `Attack()` 定义覆盖了类继承而来的版本，就好像我扩展了“boss 攻击”的含义。我本质上是在说：当 boss 攻击时，boss 会完全按照 enemy 的方式行动，然后大笑。当我在 `main()` 中使用下面这行代码为 `Boss` 对象调用该成员函数时，会调用 `Boss` 的 `Attack()` 成员函数，因为我重载了 `Attack()`。

```
aBoss.Attack();
```

`Boss` 的 `Attack()` 成员函数做的第一件事是显式调用 `Enemy` 的 `Attack()` 成员函数，后者会显示消息 “Attack! Inflicts 30 damage points.”。然后，`Boss` 的 `Attack()` 成员函数会显示消息 “And laughs heartily at you.”。

## 技巧

> 你可以通过重写基类方法，然后在这个派生类的新定义中显式调用基类成员函数并添加一些功能，来扩展基类成员函数在派生类中的工作方式。

## 在派生类中使用重载的赋值运算符和复制构造函数

你已经知道如何为一个类编写重载的赋值运算符和复制构造函数。然而，为派生类编写它们则需要更多的工作，因为它们不会从基类中继承。

当你在派生类中重载赋值运算符时，通常需要调用基类的赋值运算符成员函数，你可以使用基类名称作为前缀来显式调用它。如果 `Boss` 派生自 `Enemy`，那么在 `Boss` 中定义的重载赋值运算符成员函数可以这样开头：

```
Boss& operator=(const Boss& b)
{
    Enemy::operator=(b);    //handles the data members inherited from Enemy
    //now take care of data members defined in Boss
```

对 `Enemy` 的赋值运算符成员函数的显式调用处理了从 `Enemy` 继承的数据成员。成员函数的其余部分将处理在 `Boss` 中定义的数据成员。

对于复制构造函数，你通常也需要调用基类的复制构造函数，你可以像调用任何基类构造函数一样调用它。如果 `Boss` 派生自 `Enemy`，那么在 `Boss` 中定义的复制构造函数可以这样开头：

```
Boss (const Boss& b): Enemy(b)  //handles the data members inherited from Enemy
{
    //now take care of data members defined in Boss
```

通过使用 `Enemy(b)` 调用 `Enemy` 的复制构造函数，你可以将 `Enemy` 的数据成员复制到新的 `Boss` 对象中。在 `Boss` 的复制构造函数的其余部分，你可以处理将在 `Boss` 中声明的数据成员复制到新对象中。

## 引入多态

OOP 的支柱之一是多态，这意味着一个成员函数会根据调用它的对象类型而产生不同的结果。例如，假设玩家面对的是一群坏蛋，而这群坏蛋由通过继承关联的不同类型的对象组成，比如敌人和 Boss。借助多态的神奇力量，你可以为这群坏蛋中的每一个对象调用同一个成员函数（比如攻击玩家），而每个对象的类型将决定确切的结果。对敌人对象的调用可以产生一种结果，比如一次微弱的攻击；而对 Boss 对象的调用则可以产生另一种结果，比如一次强力的攻击。这听起来很像重写，但多态是不同的，因为函数调用的效果是动态的，是在运行时根据对象类型决定的。但理解这一点的最好方式不是通过理论讨论，而是通过一个具体的例子。

## 介绍多态坏蛋程序

Polymorphic Bad Guy 程序演示了如何实现多态行为。它展示了当你使用指向基类的指针来调用继承的虚成员函数时会发生什么。它还展示了使用虚析构函数如何确保基类指针所指向的对象调用正确的析构函数。图 10.4 显示了程序的结果。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载该程序的代码。该程序位于 Chapter 10 文件夹中；文件名是 polymorphic_bad_guy.cpp。

