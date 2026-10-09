
```cpp
void Boss::SpecialAttack() const
{
    cout << "Special Attack inflicts " << (m_DamageMultiplier * m_Damage) << " damage points!";
}

int main()
{
    cout << "Creating an enemy\n";
    Enemy enemy1;
    enemy1.Attack();

    cout << "\nCreating a boss.\n";
    Boss boss1;
    boss1.Attack();
    boss1.SpecialAttack();

    return 0;
}
```

# 从基类派生

当我通过以下行定义 `Boss` 类时，我从 `Enemy` 派了 `Boss` 类：

`class Boss : public Enemy`

事实上，`Enemy` 被称为基类（超类），而 `Boss` 是派生类（子类）。这意味着 `Boss` 继承了 `Enemy` 的数据成员和成员函数，受访问控制的影响。在这种情况下，`Boss` 继承并可以直接访问 `m_Damage` 和 `Attack()`。这就像我在 `Boss` 中同时定义了 `m_Damage` 和 `Attack()` 一样。

## 提示

你可能注意到我将所有成员（包括数据成员）都设为了 `public`。我这样做是为了使基类和派生类的示例尽可能简单。你可能还注意到我在从 `Enemy` 派生 `Boss` 时使用了 `public` 关键字。目前先不用担心这一点，我将在下一个示例 `Simple Boss 2.0` 中介绍它。

要派生你自己的类，请遵循我的示例：在类定义的类名后，跟一个冒号，然后跟一个访问修饰符（如 `public`），最后是基类的名称。从派生类派生新类是完全可以接受的，有时这样做是有意义的。然而，为了保持简单，我将只处理一层继承。

有些没有被派生类继承的基类成员需要在你在派生类中编写自己的版本，例如：

- 构造函数
- 析构函数
- 重载赋值运算符

# 从基类派实例化对象

在 `main()` 中，我实例化了一个 `Enemy` 对象并调用它的 `Attack()` 成员函数。这正如你预期的那样工作。有趣的部分开始了，当我实例化 `Boss` 对象时：

`Boss boss1;`

在这行代码之后，我拥有了一个 `m_Damage` 等于 10 且 `m_DamageMultiplier` 等于 3 的 `Boss` 对象。这一切是如何发生的？虽然构造函数和析构函数没有继承自基类，但在实例化或销毁时它们会被调用。事实上，在实例化 `Boss` 对象时，基类构造函数被调用，并赋予了 `m_Damage` 成员值 10（就像任何 `Enemy` 对象一样）。然后派生类构造函数被完成对象。在程序结束时，情况反过来。由于我没有在程序中定义析构函数，在 `Boss` 对象消失之前没有发生特殊的事情。首先调用 `Boss` 类析构函数，然后调用 `Enemy` 类析构函数。

# 使用继承的成员

接下来，我调用了 `Boss` 对象的继承成员函数，它显示了与 `enemy1.Attack()` 完全相同的消息。

```
boss1.Attack();
```

这完全合理，因为执行的是相同的代码，并且两个对象都拥有 `m_Damage` 等于 10 的数据成员。注意，函数调用方式与对 `enemy1` 时一样。`Boss` 继承成员函数这一事实对调用方式没有影响。

接下来，我让 `Boss` 发出它的特殊攻击，显示了“Special Attack inflicts 30 damage points!”的消息。

```cpp
boss1.SpecialAttack();
```

你需要注意的是，`SpecialAttack()` 定义在 `Boss` 中，但使用了在 `Enemy` 中定义的数据成员 `m_Damage`。这完全没。`Boss` 继承 `m_Damage`，在这个示例中，该数据成员的用法就像 `Boss` 类中的任何其他数据成员一样。

# 继承中的访问控制

当你从一个类派生另一个类时，你可以控制派生类对基类成员的访问权限。正如你希望向程序的其他部分提供类成员提供尽可能少的信息一样，你也希望向派生类提供类成员提供尽可能少的信息。这并非巧合，你使用了之前见过的访问修饰符——`public`、`protected` 和 `private`。（好吧，你之前还没见过 `protected`，但我将在接后的“在类成员中使用访问修饰符”章节中解释它。）

# 介绍 Simple Boss 2.0 程序

Simple Boss 2.0 程序是本章早期出现的 Simple Boss 程序的另一个版本。新版本 Simple Boss 2.0 在用户看来完全一模一样，但代码略有不同，因为我对基类成员设置了一些限制。如果你想看该程序实现的功能，请回看图 10.2。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载该程序的代码。程序位于第 10 文件夹中；文件名为 `simple_boss2.cpp`。

```cpp
//Simple Boss 2.0
// 演示继承下的访问控制

#include <iostream>
using namespace std;

class Enemy {
public:
    Enemy();
    void Attack() const;

protected:
    int m_Damage;
};

Enemy::Enemy() : m_Damage(10) {
}

void Enemy::Attack() const {
    cout << "Attack inflicts " << m_Damage << " damage points!\n";
}
```

```cpp
class Boss : public Enemy {
public:
    Boss();
    void SpecialAttack() const;

private:
    int m_DamageMultiplier;
};

Boss::Boss() : m_DamageMultiplier(3) {
}

void Boss::SpecialAttack() 
{
    cout << "Special Attack inflicts " << (m_DamageMultiplier * m_Damage);
    cout << " damage points!\n";
}

int main()
{
    cout << "\Creating an enemy.\n";
    Enemy enemy1;
    enemy1.Attack();

    cout << "\nCreating a boss.\n";
    Boss boss1;
    boss1.Attack();
    boss1.SpecialAttack();

    return 0;
}
```

# 在类成员中使用访问修饰符

你之前见过过用于类成员的 `public` 和 `private` 访问修饰符，但还有第三种可以用于类成员的修饰符——`protected`。我在 `Enemy` 的数据成员使用了它。

```cpp
protected:
int m_Damage;
```

被指定为 `protected` 的成员在类外部无法访问，但某些继承情况除外。作为复习，这里是成员访问的三个级别：

- `public` 成员对程序中的所有代码都可见。
- `protected` 成员仅在自己的类和某些派生类中可见，具体取决于继承时使用的访问级别。
- `private` 成员仅在自己的类中可见，这意味着它们在任何派生类中都无法直接访问。

# 在派生类时使用访问修饰符

当你从现有类派生一个类时，可以使用访问修饰符，例如 `public`，我在派生 `Boss` 时使用了它。

```cpp
class Boss : public Enemy
```

使用 `public` 派生意味着基类中的 `public` 成员变为派生类中的 `public` 成员，基类的 `protected` 成员变为派生类中的 `protected` 成员，而基类的 `private` 成员在派生类中不可访问。

## 技巧

> 即使数据成员是 `private` 的，你仍然可以通过基类成员函数间接使用它们。如果基类有访问器成员函数，你甚至可以获取和设置它们的值。

由于 `Boss` 使用 `public` 关键字继承自 `Enemy`，因此 `Boss` 继承了 `Enemy` 的公有成员函数作为公有成员函数。这意味着 `Boss` 将 `m_Damage` 作为 `protected` 数据成员继承了过来。该类本质上就像我直接将这两个 `Enemy` 类成员的代码直接复制并粘贴到 `Boss` 的定义中一样。但通过继承的魅力，我不需要这样做。结果是 `Boss` 类可以访问 `Attack()` 和 `m_Damage()`。

## 提示

> 你可以使用 `protected` 和 `private` 关键字派生新类，但它们很少被使用，且超出了本书的范围。

# 调用和重写基类成员函数

你并不是被局限于在派生类中使用继承的每一个基类成员函数。你有多种选项可以自定义这些继承的成员函数在派生类中的工作方式。你可以通过在派生类中为它们提供新的定义来重写它们。你也可以从派生类的任何成员函数中显式调用类成员函数。

# 引入重写 Boss 程序

`Overriding Boss` 程序演示了在派生类中调用和重写基类成员函数。该程序创建了一个嘲讽玩家并攻击他的敌人。接下来，程序从派生类创建了一个 Boss（老板）。Boss 也会嘲讽玩家并攻击他，但有趣的是，嘲讽和攻击的继承行为对于 Boss 来说发生了改变（Boss 比敌人更狡猾）。这些更改通过函数重写和调用基类函数实现。

**图 10.3** `Boss` 类继承并重写了基类函数 `Taunt()` 和 `Attack()`，为 `Boss` 中的函数创建了新的行为。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载该程序的代码。程序位于第 10 文件夹中；文件名为 `overriding_boss.cpp`。

```cpp
//Overriding Boss
// 演示调用和重写基类函数

#include <iostream>

using namespace std;

class Enemy
{
public:
    Enemy(int damage = 10);
    virtual void Taunt() const; // 设置为 virtual以便重写
    virtual void Attack() const; // 设置为 virtual以便重写

private:
    int m_Damage;
};

Enemy::Enemy(int damage): m_Damage(damage)
{
}

void Enemy::Taunt() const
{
    cout << "The enemy says he will fight you.\n";
}

void Enemy::Attack() const
{
    cout << "Attack inflicts " << m_Damage << " damage points!\n";
}

class Boss : public Enemy
{
public:
    Boss(int damage = 30);
    virtual void Taunt() const;
    virtual void Attack() const;
};

Boss::Boss(int damage): Enemy(damage)
{
}

void Boss::Taunt() const
{
    cout << "The boss says he will end you.\n";
}

void Boss::Attack() const
{
    Enemy::Attack(); // 调用基类函数
    cout << "And laughs heartily at you.\n";
}

int main()
{
    cout << "\Creating an enemy.\n";
    Enemy enemy1;
    enemy1.Taunt();
    enemy1.Attack();

    cout << "\nCreating a boss.\n";
    Boss boss1;
    boss1.Taunt();
    boss1.Attack();

    return 0;
}
```

```cpp
{
  cout << "The Boss says he will end your pitiful existence.\n";
}
```

当我通过任何 Boss 对象调用成员函数时，就会执行这个新定义。它替换了所有 Boss 对象中继承自 Enemy 的 `Taunt()` 定义。当我在 `main()` 中通过以下行调用成员函数时，会显示消息“Boss 说他将结束你可怜的生命”。

```cpp
aBoss.Taunt();
```

当你想要在派生类中更改或扩展基类成员函数的行为时，重写成员函数是非常用的。

## 陷阱 (Trap)

不要将重写（override）与重载（overload）混淆。当你重写一个成员函数时，你是在派生类中为它提供了一个新的定义。当你重载一个函数时，你是在创建它的具有不同签名的多个版本。

## 陷阱 (Trap)

当你重写一个重载的基类成员函数时，你会隐藏掉所有的重载版本——这意味着访问该成员函数其他版本的唯一方法是显式地调用基类成员函数。因此，如果你重写了一个重载的成员函数，最好重写该重载函数的每一个版本。

## 调用基类成员函数 (Calling Base Class Member Functions)

你可以从派生类的中的任何函数直接调用基类成员函数。你所做的只是使用作用域解析运算符在成员函数前加上类名。这正我在为 `Boss` 类定义 `Attack()` 的重写版本时所做的。

```cpp
void Boss::Attack() const //重写基类成员函数{
  Enemy::Attack(); //调用基类成员函数
  cout << " And laughs heartily at you.\n"
}
```

代码 `Enemy::Attack();` 显式地调用了 `Enemy` 的 `Attack()` 成员函数。由于 `Boss` 中的 `Attack()` 定义重写了继承的版本，这就像是我扩展了 Boss 攻击的含义的定义。我本质上说说，当 Boss 攻击时，Boss 执行了与敌人完全相同的操作并大笑。当我在 `main()` 中通过以下行调用 Boss 对象的成员函数时，调用的是 Boss 的 `Attack()` 成员函数，因为我重载了 `Attack()`。

```cpp
aBoss.Attack();
```

Boss 的 `Attack()` 成员函数执行的第一件事是显式调用 `Enemy` 的 `Attack()` 成员函数，它显示消息“攻击！造成了 30 点伤害。”然后，Boss 的 `Attack()` 成员函数显示消息“并对你大笑”。

## 技巧 (Trick)

你可以通过重写基类方法，并在派生类的这个新定义中显式调用基类成员函数并添加某些功能，从而派生类中扩展基类成员函数的功能。

## 在派生类中使用重载赋值运算符和拷贝构造函数 (USING OVERLOADED ASSIGNMENT OPERATORS AND COPY CONSTRUCTORS IN DERIVED CLASSES)

你已经知道如何为类编写重载的赋值运算符和拷贝构造函数。然而，为派生类编写它们需要一些额外的工作，因为它们不是继承自基类。

当你在派生类中重载赋值运算符时，你通常想要调用基类的赋值运算符成员函数，你可以使用基类名作为前缀显式调用它。如果 `Boss` 派自 `Enemy`，那么在 `Boss` 中定义的重载赋值运算符成员函数可以：

```cpp
Boss& operator=(const Boss& b)
{
  Enemy::operator=(b); //处理继承自 Enemy 的数据成员
  //处理 Boss 中定义的数据成员
}
```

对 `Enemy` 赋值运算符成员函数的显式调用处理了继承自 `Enemy` 的数据成员。成员函数的其余部分将处理 `Boss` 中定义的数据成员。

## 引入多态 (Introducing Polymorphism)

对于拷贝构造函数，你通常也想要调用基类的拷贝构造函数，你可以像调用任何基类构造函数一样调用它。如果 `Boss` 派自 `Enemy`，`Boss` 中定义的拷贝构造函数可以这样：

```cpp
Boss (const Boss& b): Enemy(b) //处理继承自 Enemy 的数据成员
{}
```

通过用 `Enemy(b)` 调用 `Enemy` 的拷贝构造函数，你将 `Enemy` 的数据成员拷贝到新的 `Boss` 对象中。在 `Boss` 拷贝构造函数的剩余部分，你可以处理将 `Boss` 中声明的数据成员拷贝到新对象中。

## 引入多态

面向对象编程（OOP）支柱之一是多态，这意味着成员函数将根据调用它的对象类型产生不同的结果。例如，假设你有一组玩家正面对付的坏蛋，这组是由通过继承相关的不同类型对象组成的，例如敌人和 Boss。通过多态的魔力，你可以为组中的每个坏蛋调用同一个成员函数，每个对象的类型将决定确切的结果。对敌人对象的调用可能会产生一个结果（例如弱攻击），而对 Boss 的调用可能会产生另一个结果（例如强力攻击）。这听起来很像重写，但多态是不同的，因为函数的副作用是动态的，并且是在运行时根据对象类型确定的。理解这一点的最佳方法不是通过理论讨论，而是通过一个具体的例子。

## 引入多态坏蛋程序 (Introducing the Polymorphic Bad Guy Program)
