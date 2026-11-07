
类的定义。在构造函数的定义头部，我们没有指定默认值。构造函数的定义如下：

```cpp
cashRegister::cashRegister(int cashIn)
{
    if (cashIn >= 0)
        cashOnHand = cashIn;
    else
        cashOnHand = 500;
}
```

请注意，构造函数的定义会检查参数 cashIn 的有效值。如果 cashIn 的值小于 0，则赋给成员变量 cashOnHand 的值为 500。

## 售货机

售货机在非空时放出所选物品。它应显示售货机中物品的数量以及物品的成本。下面的类定义了售货机的属性。我们称这个类为 dispenserType：

```cpp
class dispenserType
{
public:
    int getNoOfItems() const;
        //Function to show the number of items in the machine.
        //Postcondition: The value of numberOfItems is returned.

    int getCost() const;
        //Function to show the cost of the item.
        //Postcondition: The value of cost is returned.

    void makeSale();
        //Function to reduce the number of items by 1.
        //Postcondition: numberOfItems--;

    dispenserType(int setNoOfItems = 50, int setCost = 50);
        //Constructor
        //Sets the cost and number of items in the dispenser
        //to the values specified by the user.
        //Postcondition: numberOfItems = setNoOfItems;
        //              cost = setCost;
        //              If no value is specified for a
        //              parameter, its default value is
        //              assigned to the corresponding member
        //              variable.

private:
    int numberOfItems;  //Variable to store the number of
                        //items in the dispenser
    int cost;           //Variable to store the cost of an item
};
```

图 10-16 显示了 `class dispenserType` 的 UML 类图。

![](img/d0be7fc6d804b63484835c6c8bc67a07_758_0.png)

**图 10-16** `class dispenserType` 的 UML 类图

因为果汁机销售四种物品，我们将声明四个 `dispenserType` 类型的对象。例如，语句：

```cpp
dispenserType apple(100, 65);
```

将 apple 声明为 `dispenserType` 类型的对象，将售货机中苹果汁瓶的数量设置为 100，并将每瓶苹果汁的成本设置为 65 美分（见图 10-17）。

![](img/d0be7fc6d804b63484835c6c8bc67a07_758_1.png)

**图 10-17** 对象 `apple`

接下来，我们讨论实现 `class dispenserType` 操作的函数定义。

函数 `getNoOfItems` 返回特定产品的物品数量。由于售货机中当前的物品数量存储在 `private` 成员变量 `numberOfItems` 中，因此该函数返回 `numberOfItems` 的值。此函数的定义是：

```cpp
int dispenserType::getNoOfItems() const
{
    return numberOfItems;
}
```

函数 `getCost` 返回产品的成本。由于产品的成本存储在 `private` 成员变量 `cost` 中，因此该函数返回 `cost` 的值。此函数的定义是：

```cpp
int dispenserType::getCost() const
{
    return cost;
}
```

当产品售出时，该售货机中的物品数量减少 1。因此，函数 `makeSale` 将售货机中的物品数量减少 1。也就是说，它将 `private` 成员变量 `numberOfItems` 的值减 1。此函数的定义是：

```cpp
void dispenserType::makeSale()
{
    numberOfItems--;
}
```

构造函数的定义检查参数值是否有效。如果这些值小于 0，则将默认值赋给成员变量。构造函数的定义是：

```cpp
//constructor
dispenserType::dispenserType(int setNoOfItems, int setCost)
{
    if (setNoOfItems >= 0)
        numberOfItems = setNoOfItems;
    else
        numberOfItems = 50;

    if (setCost >= 0)
        cost = setCost;
    else
        cost = 50;
}
```

## 主程序

程序执行时，必须完成以下操作：

- 1. 显示果汁机销售的不同产品。
- 2. 显示如何选择特定产品。
- 3. 显示如何终止程序。

此外，这些指令必须在处理完每次选择后显示（退出程序除外），这样用户如果想购买两件或更多物品，就不必记住该怎么做。一旦用户做出适当的选择，果汁机必须相应地采取行动。如果用户选择购买某产品且该产品有货，果汁机应显示该产品的成本，并要求用户投入钱币。如果投入的金额至少等于该物品的成本，果汁机应售出该物品并显示相应的信息。

用伪代码表示，该函数的算法如下：

- 1. 如果售货机不为空，
  - a. 显示并提示顾客输入该物品的成本。
  - b. 获取顾客输入的金额。
  - c. 如果顾客输入的金额小于产品的成本，
    - i. 显示并提示顾客输入额外金额。
    - ii. 计算顾客输入的总额。
  - d. 如果顾客输入的金额至少等于产品的成本，
    - i. 通过加上用户输入的金额来更新收银机中的金额。
    - ii. 售出产品——也就是说，将售货机中的物品数量减 1。
    - iii. 显示相应的信息。
  - e. 如果用户输入的金额小于该物品的成本，退回该金额。
- 2. 如果售货机为空，告诉用户该产品已售罄。

sellProduct 函数的定义如下：

```cpp
void sellProduct(dispenserType product,
                 cashRegister& pCounter)
{
    int amount;   //variable to hold the amount entered
    int amount2;  //variable to hold the extra amount needed

    if (product.getNoOfItems() > 0)  //if the dispenser is not
                                    //empty
    {
        cout << "Please deposit " << product.getCost()
             << " cents" << endl;
        cin >> amount;

        if (amount < product.getCost())
        {
            cout << "Please deposit another "
                 << product.getCost() - amount
                 << " cents" << endl;
            cin >> amount2;
            amount = amount + amount2;
        }

        if (amount >= product.getCost())
        {
            pCounter.acceptAmount(amount);
            product.makeSale();
            cout << "Collect your item at the bottom and "
                 << "enjoy." << endl;
        }
        else
            cout << "The amount is not enough. "
                 << "Collect what you deposited." << endl;

        cout << "*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*"
             << endl << endl;
    }
    else
        cout << "Sorry, this item is sold out." << endl;
}//end sellProduct
```

![](img/d0be7fc6d804b63484835c6c8bc67a07_761_0.png)

现在我们已经描述了函数 showSelection 和 sellProduct，下面将描述函数 main。

函数 main 的算法如下：

- 1. 创建收银机——也就是说，声明一个 `cashRegister` 类型的对象。
- 2. 创建四个售货机——也就是说，声明四个 `dispenserType` 类型的对象并初始化这些对象。例如，语句：
  `dispenserType orange(100, 50);`
  创建一个售货机对象，用于存放果汁。售货机中的物品数量为 100，每个物品的成本为 50 美分。
- 3. 根据需要声明其他变量。
- 4. 显示选择；调用函数 `showSelection`。
- 5. 获取选择。
- 6. 当尚未完成时（选择 9 退出程序），
  - a. 售出产品；调用函数 `sellProduct`。
  - b. 显示选择；调用函数 `showSelection`。
  - c. 获取选择。

函数 main 的定义如下：

```cpp
int main()
{
    cashRegister counter;
    dispenserType orange(100, 50);
    dispenserType apple(100, 65);
```

