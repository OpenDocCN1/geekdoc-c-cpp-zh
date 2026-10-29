

接下来，定义一个名为 `CashPayment` 的类，它继承自 `Payment`。该类应重新定义 `paymentDetails` 函数，以表明该支付为现金支付。请包含适当的构造函数。

定义一个名为 `CreditCardPayment` 的类，它继承自 `Payment`。该类应包含用于存储持卡人姓名、到期日期和信用卡号的成员变量。请包含适当的构造函数。最后，重新定义 `paymentDetails` 函数，以便在打印输出中包含所有信用卡信息。

创建一个 `main` 函数，创建至少两个 `CashPayment` 和两个 `CreditCardPayment` 对象，并使用不同的值，然后为每个对象调用 `paymentDetails`。

## 7.

定义一个名为 `Document` 的类，其中包含一个名为 `text` 的字符串类型成员变量，用于存储文档的任何文本内容。创建一个名为 `getText` 的函数来返回 `text` 字段，提供一种设置此值的方法，以及一个重载的赋值运算符。

接下来，定义一个名为 `Email` 的类，它继承自 `Document`，并包含用于存储电子邮件发件人、收件人和标题的成员变量。实现适当的访问器和修改器函数。电子邮件的正文应存储在继承的变量 `text` 中。同时重载此类的赋值运算符。

类似地，定义一个名为 `File` 的类，它继承自 `Document`，并包含一个用于存储路径名的成员变量。为路径名实现适当的访问器和修改器函数，并重载赋值运算符。

最后，在你的 `main` 函数中创建几个 `Email` 和 `File` 类型的示例对象。通过将它们传递给以下子程序来测试你的对象，如果对象在 `text` 属性中包含指定的关键字，该子程序将返回 `true`。

```
bool ContainsKeyword(const Document& docObject, string keyword)
{
    if (docObject.getText().find(keyword) != string::npos)
        return true;
    return false;
}
```

例如，你可以通过调用 `ContainsKeyword(emailObj, "c++")` 来测试电子邮件消息是否包含文本 "c++"。

## 8.

为一个简单的博客创建一个类。博客的所有者应该能够 (a) 发布新消息，(b) 以数字列表形式列出并显示所有消息，以及 (c) 选择特定消息并将其删除。

博客的浏览者应该只能以数字列表形式列出并显示所有已发布的消息。

创建一个 `Viewer` 类和一个 `Owner` 类，使用继承来帮助实现博客功能。使用你喜欢的任何格式存储数据消息（字符串类型的向量可能最简单）。应为每个类实现一个菜单函数，输出该类型用户的合法选项。为了测试你的类，程序的 `main` 函数应允许用户从 `Viewer` 和 `Owner` 对象调用菜单。

## 9.

假设你正在创建一个奇幻角色扮演游戏。在这个游戏中，我们有四种不同类型的生物：人类、网络恶魔、炎魔和精灵。为了表示其中一种生物，我们可以如下定义一个 `Creature` 类：

```
class Creature
{
    private:
        int type;    // 0 人类, 1 网络恶魔, 2 炎魔, 3 精灵
        int strength;    // 我们能造成的伤害量
        int hitpoints;   // 我们能承受的伤害量
        string getSpecies(); // 返回物种类型
    public:
        Creature();
        // 初始化为人类，10 点力量，10 点生命值
        Creature(int newType, int newStrength, int newHit);
        // 将生物初始化为新的类型、力量、生命值
        // 同时为类型、力量和生命值添加适当的访问器和修改器函数
        int getDamage();
        // 返回该生物在一轮战斗中
        // 造成的伤害量
};
```

以下是 `getSpecies()` 函数的实现：

```
string Creature::getSpecies()
{
    switch (type)
    {
        case 0: return "Human";
        case 1: return "Cyberdemon";
        case 2: return "Balrog";
        case 3: return "Elf";
    }
    return "Unknown";
}
```

`getDamage()` 函数输出并返回该生物在一轮战斗中能造成的伤害。计算伤害的规则如下：

- 每个生物造成的伤害是一个随机数 `r`，其中 `0 < r <= strength`。
- 恶魔有 5% 的几率发动恶魔攻击，额外造成 50 点伤害。炎魔和网络恶魔属于恶魔。
- 精灵有 10% 的几率发动魔法攻击，使正常伤害翻倍。
- 炎魔速度非常快，因此它们可以攻击两次。

`getDamage()` 的一个实现如下：

```
int Creature::getDamage()
{
    int damage;

    // 所有生物都会造成伤害，这是一个
    // 不超过其力量值的随机数
    damage = (rand() % strength) + 1;
    cout << getSpecies() << " attacks for " <<
            damage << " points!" << endl;

    // 恶魔有 5% 的几率造成 50 点伤害
    if ((type == 2) || (type == 1))
    {
        if ((rand() % 100) < 5)
        {
            damage = damage + 50;
            cout << "Demon attack inflicts 50 "
                    << " additional damage points!" << endl;
        }
    }

    // 精灵有 10% 的几率造成双倍魔法伤害
    if (type == 3)
    {
        if ((rand() % 10)==0)
        {
            cout << "Magical attack inflicts " << damage <<
                    " additional damage points!" << endl;
            damage = damage * 2;
        }
    }

    // 炎魔速度极快，可以攻击两次
    if (type == 2)
    {
        int damage2 = (rand() % strength) + 1;
        cout << "Balrog speed attack inflicts " << damage2 <<
                " additional damage points!" << endl;

        damage = damage + damage2;
    }
    return damage;
}
```

这个实现的一个问题是添加新生物很不方便。重写该类以使用继承，这将消除对 `type` 变量的需求。`Creature` 类应为基类。`Demon`、`Elf` 和 `Human` 类应派生自 `Creature`。`Cyberdemon` 和 `Balrog` 类应派生自 `Demon`。你需要重写 `getSpecies()` 和 `getDamage()` 函数，使其适用于每个类。

例如，每个类中的 `getDamage()` 函数应仅计算该对象对应的伤害。然后通过组合继承层次结构中每一层的 `getDamage()` 结果来计算总伤害。例如，为 `Balrog` 对象调用 `getDamage()` 应调用 `Demon` 对象的 `getDamage()`，后者又应调用 `Creature` 对象的 `getDamage()`。这将计算所有生物造成的基础伤害，然后是恶魔造成的随机 5% 伤害，最后是炎魔造成的双倍伤害。

同时为私有变量包含修改器和访问器函数。编写一个 `main` 函数，其中包含一个驱动程序来测试你的类。它应为每种生物类型创建一个对象，并重复输出 `getDamage()` 的结果。

## 10.

定义一个 `Pet` 类，用于存储宠物的名字、年龄和体重。添加适当的构造函数、访问器函数和修改器函数。同时定义一个名为 `getLifespan` 的函数，返回字符串 "unknown lifespan"。

接下来，定义一个名为 `Dog` 的类，它派生自 `Pet`。`Dog` 类应有一个名为 `breed` 的私有成员变量，用于存储狗的品种。为 `breed` 变量添加修改器和访问器函数以及适当的构造函数。重新定义 `getLifespan` 函数，如果狗的体重超过 100 磅，则返回 "Approximately 7 years"；如果狗的体重低于 100 磅，则返回 "Approximately 13 years"。

接下来，定义一个名为 `Rock` 的类，它派生自 `Pet`。重新定义 `getLifespan` 函数，返回 "Thousands of years"。

最后，编写一个测试程序，创建宠物岩石和宠物狗的实例，以练习继承的和重新定义的函数。

## 11.

使用继承和类来表示一副扑克牌。创建一个 `Card` 类，存储花色（梅花、方块、红心、黑桃）和名称（例如，A、2、10、J），并附带适当的访问器、构造函数和修改器。

接下来，创建一个 `Deck` 类，存储一个 `Card` 对象的向量。默认构造函数应创建代表标准 52 张牌的对象并将它们存储在向量中。`Deck` 类应具有以下功能：

- 打印牌组中的每张牌。
- 洗牌。你可以通过随机交换牌组中的每张牌来实现。
- 向牌组中添加一张新牌。此函数应将一个 `Card` 对象作为参数并将其添加到向量中。
- 从牌组中移除一张牌。这会移除向量中存储的第一张牌并将其返回。
- 按名称对牌组中的牌进行排序。

