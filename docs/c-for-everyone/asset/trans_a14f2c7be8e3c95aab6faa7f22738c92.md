

```
public:
    Item(string item_description, double item_price);
    // No other constructors
    ...
};
```

这个 Order 类有一个 Item 类型的数据成员：

```
class Order
{
public:
    Order(string customer_name, string item_description, double item_price);
    ...
private:
    Item article;
    string customer;
};
```

Order 构造函数必须调用 Item 构造函数。这可以通过*初始化列表*实现。初始化列表位于构造函数左大括号之前。列表以冒号开头，并包含数据成员的名称及其构造参数。

```
Order(string customer_name, string item_description, double item_price)
    : article(item_description, item_price)
{
    customer = customer_name;
}
```

初始化项之间用逗号分隔。Order 构造函数也可以写成这样：

```
Order(string customer_name, string item_description, double item_price)
    : article(item_description, item_price), customer(customer_name)
{
}
```

初始化项之间用逗号分隔。Order 构造函数也可以写成这样：

```
Order(string customer_name, string item_description, double item_price)
    : article(item_description, item_price), customer(customer_name)
{
}
```

### 专题 9.2

![](img/5e58fb4c840712efd6ed6fa82bb97f57_433_0.png)

### 重载

当同一个函数名用于多个函数时，这个名称就是**重载的**。在 C++ 中，只要参数变量的类型不同，就可以重载函数名。例如，可以定义两个都名为 print 的函数：

```
void print(CashRegister r);
void print(Item i);
```

调用 print 函数时，

```
print(x);
```

编译器会查看 x 的类型。如果 x 是 CashRegister 对象，就调用第一个函数。如果 x 是 Item 对象，就调用第二个函数。如果 x 两者都不是，编译器就会生成错误。

通过为每个函数指定唯一的名称（例如 print_register 或 print_item），总是可以避免重载。不过，对于构造函数，我们别无选择。C++ 要求构造函数的名称必须与类名相同。如果一个类有多个构造函数，那么这个名称就必须进行重载。

除了名称重载之外，C++ 还支持**运算符重载**。可以为熟悉的 C++ 运算符（如 +、-= 和 <<）赋予新的含义。这是一种高级技术，本书不予讨论。

### 9.6 问题求解：跟踪对象

> 将成员函数写在卡片正面，将数据成员的值写在卡片背面。

你已经看到，手动跟踪技术对于理解程序的运行方式非常有用。当程序包含对象时，可以调整这种技术，从而更好地理解对象数据和封装。

为每个对象使用一张索引卡或便签。在正面写下对象可以执行的成员函数。在背面为数据成员的值制作一张表。

下面是一张 CashRegister 对象的卡片：

![](img/5e58fb4c840712efd6ed6fa82bb97f57_434_0.png)

![](img/5e58fb4c840712efd6ed6fa82bb97f57_434_1.png)

*正面*

*背面*

这可以让你以一种简单的方式感受封装。对象通过其公共接口（位于卡片正面）进行操作，而数据成员则隐藏在卡片背面。

构造对象时，填写数据成员的初始值。

| item_count | total_price |
|---:|---:|
| 0 | 0 |

> 调用修改器成员函数时，更新数据成员的值。

每当执行修改器成员函数时，划掉旧值，并在下面写入新值。调用 add_item 成员函数后，情况如下：

| item_count | total_price |
|---:|---:|
| ~~0~~ | ~~0~~ |
| 1 | 19.95 |

如果程序中有多个对象，就会有多张卡片，每个对象对应一张：

| item_count | total_price |
|---|---|
| 0 | 0.0 |
| 1 | 19.95 |

| item_count | total_price |
|---|---|
| 0 | 0.0 |
| 1 | 19.95 |
| 2 | 14.90 |

在设计类时，这些图示同样很有用。假设要求你增强 CashRegister 类，使其能够计算销售税。将 get_sales_tax 函数添加到卡片正面。现在将卡片翻过来，查看数据成员，并问问自己：对象是否拥有计算结果所需的足够信息？记住，每个对象都是一个自主单元。任何可用于计算的数据值都必须是：

- 数据成员。
- 函数参数。
- 全局常量或变量。

为了计算销售税，我们需要知道税率和应税商品的总额。（食品通常不需要缴纳销售税。）目前我们没有这些信息。让我们为税率和应税总额引入额外的数据成员。税率可以在构造函数中设置（假设对象的整个生命周期内税率保持不变）。添加商品时，需要告知我们该商品是否应税。如果应税，就将其价格加到应税总额中。

例如，考虑以下语句。

```
    CashRegister reg2(7.5); // 7.5 percent sales tax
    reg2.add_item(3.95, false); // not taxable
    reg2.add_item(19.95, true); // taxable
```

将执行结果记录在卡片上后，如下所示：

| item_count | total_price | taxable_total | tax_rate |
|---|---|---|---|
| 0 | 0.0 | 0.0 | 7.5 |
| 1 | 3.95 | 0.0 |  |
| 2 | 23.90 | 19.95 |  |

有了这些信息，计算税额就很容易了。税额等于 taxable_total × tax_rate / 100。通过跟踪对象，我们理解了为什么需要额外的数据成员。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_435_0.png)

- 25. 考虑一个模拟汽车燃油消耗的 Car 类。我们假设汽车具有固定的效率（每加仑英里数），该效率在构造函数中提供。类中有用于加油、驾驶指定距离以及检查油箱剩余油量的成员函数。为 Car 对象制作一张卡片，选择合适的数据成员，并显示对象构造后的数据成员值。

- 26. 跟踪以下成员函数调用：

```
Car my_car(25);
my_car.add_gas(20);
my_car.drive(100);
my_car.drive(200);
my_car.add_gas(5);
```

- 27. 假设要求你通过添加 get_miles_driven 成员函数来模拟汽车的里程表。向对象的卡片中添加一个适合计算该成员函数的数据成员。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_436_0.png)

- 28. 跟踪自测题 26 中的成员函数，并更新自测题 27 中添加的数据成员。

**动手练习** 现在，你可以尝试本章末尾的以下练习：R9.20、R9.21、R9.22。

### 操作指南 9.1 实现一个类

![](img/5e58fb4c840712efd6ed6fa82bb97f57_436_1.png)

实现一个类，使其对象能够执行一组指定的操作，是一项非常常见的任务。本操作指南将带你逐步完成必要的步骤。

例如，考虑一个 Menu 类。该类的对象可以显示如下菜单：

- 1) 开设新账户
- 2) 登录现有账户
- 3) 帮助
- 4) 退出

然后，菜单等待用户提供一个值。如果用户提供的值无效，菜单就会重新显示，用户可以再次尝试。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_436_2.png)

**步骤 1** 列出对象所承担职责的非正式清单。

注意，要将范围限制在问题实际要求的功能上。对于现金收款机或银行账户等现实世界中的对象，可能有几十项值得实现的功能。然而，你的任务并不是忠实地模拟现实世界。你只需要确定解决具体问题所需的职责。

在菜单的例子中，你需要：

- **显示菜单。**
- **获取用户输入。**

现在寻找问题描述中没有明确提到的隐藏职责。对象是如何创建的？哪些日常活动需要执行，例如在每次销售开始时清空现金收款机？

在菜单示例中，考虑菜单是如何生成的。程序员创建一个空菜单对象，然后添加“开设新账户”“帮助”等选项。这里存在一个隐藏职责：

- **添加选项。**

**步骤 2** 指定公共接口。

将步骤 1 中的清单转换为一组成员函数，并为参数变量和返回值指定具体类型。务必将访问器标记为 const。许多程序员发现

