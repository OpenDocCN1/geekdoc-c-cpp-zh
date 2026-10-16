
要按照我的示例来派生出你自己的类。在类定义的类名后面，加一个冒号，后跟一个访问修饰符（如 `public`），再跟基类的名称。从派生类再派生新类是完全可行的，而且有时这么做非常有意义。不过，为了简单起见，本示例中我只处理一层继承。

实际上，有些基类成员函数不会被派生类继承，如下所示：

- 构造函数
- 拷贝构造函数
- 析构函数
- 重载的赋值运算符

你必须在派生类中自己编写这些函数的版本。

## 从派生类实例化对象

在 `main()` 中，我实例化了一个 Enemy 对象，然后调用它的 `Attack()` 成员函数。这和你预期的一样。程序接下来进入有趣的部分：当我实例化一个 Boss 对象时。

```
Boss boss1;
```

在这行代码之后，我得到了一个 `Boss` 对象，它的 `m_Damage` 数据成员等于 10，`m_DamageMultiplier` 数据成员等于 3。这是怎么发生的？虽然构造函数和析构函数不会从基类继承，但在创建或销毁实例时它们会被调用。实际上，基类构造函数会在派生类构造函数之前被调用，以创建最终对象中属于基类的部分。

在本例中，当 `Boss` 对象被实例化时，默认的 `Enemy` 构造函数会被自动调用，对象会得到一个值为 10 的 `m_Damage` 数据成员（就像任何 `Enemy` 对象一样）。然后，`Boss` 构造函数被调用，并赋予对象一个值为 3 的 `m_DamageMultiplier` 数据成员，从而完成对象的创建。在程序结束、`Boss` 对象被销毁时，顺序正好相反。首先，为该对象调用 `Boss` 类的析构函数，然后再调用 Enemy 类的析构函数。因为我在此程序中没有定义析构函数，所以在 `Boss` 对象销毁之前不会发生什么特殊的事情。

### 提示

> 对于派生类的对象会调用基类析构函数，这一事实确保了每个类都有机会清理对象中需要处理的部分，比如堆上的内存。

## 使用继承的成员

接下来，我调用 `Boss` 对象的一个继承成员函数，它会显示与 `enemy1.Attack()` 完全相同的信息。

```
boss1.Attack();
```

这完全合理，因为执行的是相同的代码，而且两个对象的 `m_Damage` 数据成员都等于 10。注意，这个函数调用的形式和 `enemy1` 的调用完全相同。`Boss` 从 `Enemy` 继承了该成员函数，这一事实对函数的调用方式没有任何影响。

接下来，我让 `Boss` 施展它的特殊攻击，会显示消息 `Special Attack inflicts 30 damage points!`

```
boss1.SpecialAttack();
```

这里需要关注的是，作为 `Boss` 的一部分而声明的 `SpecialAttack()`，使用了在 `Enemy` 中声明的数据成员 `m_Damage`。这完全没有问题。`Boss` 从 `Enemy` 继承了 `m_Damage`，在本例中，该数据成员与 `Boss` 类中的任何其他数据成员一样工作。

## 继承中的访问控制

当你从一个类派生另一个类时，你可以控制派生类对基类成员拥有多少访问权限。出于与希望向程序其余部分只提供必要的类成员访问权限相同的原因，你也希望只向派生类提供必要的类成员访问权限。并非巧合的是，你使用的是之前见过的那些访问修饰符——public、protected 和 private。（好吧，你之前还没见过 protected，但我将在“对类成员使用访问修饰符”一节中解释这个修饰符。）

## 介绍 Simple Boss 2.0 程序

Simple Boss 2.0 程序是本章前面 Simple Boss 程序的另一个版本。新版本 Simple Boss 2.0 对用户来说看起来完全相同，但代码略有不同，因为我对基类成员设置了一些限制。如果你想看看这个程序做了什么，可以回头看看图 10.2。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载此程序的代码。程序位于第 10 章文件夹中；文件名是 simple_boss2.cpp。

```
//Simple Boss 2.0
//Demonstrates access control under inheritance

#include <iostream>
using namespace std;

class Enemy
{
public:
    Enemy();
    void Attack() const;

protected:
    int m_Damage;
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
    Boss();
    void SpecialAttack() const;

private:
    int m_DamageMultiplier;
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

## 对类成员使用访问修饰符

你已经见过访问修饰符 public 和 private 用于类成员，但你还可以对类成员使用第三个修饰符——protected。这就是我用于 Enemy 的数据成员的修饰符。

```
protected:
    int m_Damage;
```

被指定为 protected 的成员不能在类外部访问，但在某些继承情况下除外。复习一下，以下是成员访问的三个级别：

- public 成员可以被程序中的所有代码访问。
- `protected` 成员只能在其自身类和某些派生类中访问，具体取决于继承中使用的访问级别。
- `private` 成员只能在其自身类中访问，这意味着在任何派生类中都不能直接访问它们。

## 派生类时使用访问修饰符

当你从一个现有类派生类时，可以使用访问修饰符，比如 `public`，我就用它来派生 `Boss`。

```
class Boss : public Enemy
```

使用 public 派生意味着基类中的 public 成员成为派生类中的 public 成员，基类中的 protected 成员成为派生类中的 protected 成员，而基类中的 private 成员在派生类中不可访问。

### 技巧

> 即使基类数据成员是 private 的，你仍然可以通过基类成员函数间接使用它们。如果基类有访问器成员函数，你甚至可以获取和设置它们的值。

因为 `Boss` 使用关键字 `public` 从 `Enemy` 继承，所以 `Boss` 将 `Enemy` 的 public 成员函数作为 public 成员函数继承。这也意味着 `Boss` 将 `m_Damage` 作为 protected 数据成员继承。这个类本质上就像是我把这两个 `Enemy` 类成员的代码直接复制粘贴到 `Boss` 定义中一样。但通过继承之美，我不必这样做。结果是 `Boss` 类可以访问 `Attack()` 和 `m_Damage()`。

### 提示

> 你可以使用 `protected` 和 `private` 关键字派生新类，但它们很少使用，并且超出了本书的范围。

## 调用和覆盖基类成员函数

你并不是只能按原样使用在派生类中继承的每个基类成员函数。你有多种选择，可以自定义这些继承的成员函数在派生类中的工作方式。你可以在派生类中为它们提供新的定义来覆盖它们。你也可以从派生类的任何成员函数中显式调用基类成员函数。

## 介绍 Overriding Boss 程序

Overriding Boss 程序演示了在派生类中调用和覆盖基类成员函数。该程序创建一个嘲弄玩家然后攻击玩家的敌人。接下来，程序从派生类创建一个 Boss。Boss 也会嘲弄玩家并攻击玩家，但有趣的是，嘲弄和攻击的继承行为对 Boss（比敌人更自大一些）来说发生了变化。这些变化是通过函数覆盖和调用基类成员函数来实现的。图 10.3 显示了程序的结果。

![](img/34f09be0ed6217c465debc4490197d4f_363_0.png)

图 10.3
Boss 类继承并覆盖了基类成员函数 Taunt() 和 Attack()，为这些函数在 Boss 中创建了新的行为。

你可以从 Course Technology 网站（www.courseptr.com/downloads）下载此程序的代码。程序位于第 10 章文件夹中；文件名是 overriding_boss.cpp。

```
//Overriding Boss
//Demonstrates calling and overriding base member functions

#include <iostream>

using namespace std;
```
