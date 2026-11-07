

图 12-16 显示了类 `dispenserType` 的 UML 类图。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_740_0.png)

**图 12-16**  类 `dispenserType` 的 UML 类图

由于糖果机销售四种商品，我们将声明四个 `dispenserType` 类型的对象。例如，以下语句：

```cpp
dispenserType chips(100, 65);
```

将 `chips` 声明为 `dispenserType` 类型的对象，将售货器中薯片袋的数量设为 100，并将每袋薯片的价格设为 65 美分（见图 12-17）。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_740_1.png)

**图 12-17**  对象 `chips`

接下来，我们讨论实现类 `dispenserType` 各操作的函数定义。

函数 `getNoOfItems` 返回特定商品的数量。由于售货器中当前的商品数量存储在私有成员变量 `numberOfItems` 中，该函数返回 `numberOfItems` 的值。该函数的定义如下：

```cpp
int dispenserType::getNoOfItems() const
{
    return numberOfItems;
}
```

函数 `getCost` 返回商品的价格。由于商品价格存储在**私有**成员变量 `cost` 中，该函数返回 `cost` 的值。该函数的定义如下：

```cpp
int dispenserType::getCost() const
{
    return cost;
}
```

当商品售出时，该售货器中的商品数量减 1。因此，函数 `makeSale` 将售货器中的商品数量减 1。也就是说，它将**私有**成员变量 `numberOfItems` 的值减 1。该函数的定义如下：

```cpp
void dispenserType::makeSale()
{
    numberOfItems--;
}
```

构造函数的定义会检查参数的有效值。如果这些值小于 0，则将默认值赋给成员变量。构造函数的定义如下：

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

程序执行时，必须执行以下操作：

- 1. 显示糖果机销售的不同商品。
- 2. 显示如何选择特定商品。
- 3. 显示如何终止程序。

此外，这些说明必须在处理每次选择后显示（退出程序除外），这样用户如果想购买两件或更多商品，就无需记住该怎么做。用户做出相应选择后，糖果机必须据此执行操作。如果用户选择购买某种商品且该商品有货，糖果机应显示该商品的价格，并要求用户投入钱款。如果投入的金额至少等于商品价格，糖果机应售出该商品并显示相应消息。

上述讨论可转化为以下算法：

- 1. 向顾客显示选择项。
- 2. 获取选择。
- 3. 如果选择有效且该选择对应的售货器不为空，则售出商品。

我们将该程序划分为三个函数：`showSelection`、`sellProduct` 和 `main`。

### showSelection

```cpp
void showSelection()
{
    cout << "*** Welcome to Shelly's Candy Shop ***" << endl;
    cout << "To select an item, enter " << endl;
    cout << "1 for Candy" << endl;
    cout << "2 for Chips" << endl;
    cout << "3 for Gum" << endl;
    cout << "4 for Cookies" << endl;
    cout << "9 to exit" << endl;
}//end showSelection
```

### sellProduct

该函数尝试售出顾客选择的商品。因此，它必须能够访问存放该商品的售货器。该函数做的第一件事是检查存放该商品的售货器是否为空。如果售货器为空，该函数会通知顾客该商品已售罄。如果售货器不为空，它会告诉用户投入购买该商品所需的金额。

如果用户投入的钱不足以购买该商品，`sellProduct` 会告诉用户还需要投入多少钱。如果用户两次尝试后仍未投入足够的钱购买该商品，该函数会直接退还钱款。（本章末尾的编程练习 9 要求你修改方法 `sellProduct` 的定义，使其在用户未投入足够购买该商品的钱时，持续要求用户输入追加金额。）如果用户投入的金额足够，它就收下钱款并售出商品。售出商品意味着将售货器中的商品数量减 1，并通过加上该商品的价格来更新收银机中的钱款。（由于该程序不会退还顾客多投入的钱，因此收银机通过加上用户输入的金额来更新。）

从上述讨论可以清楚地看出，函数 `sellProduct` 必须能够访问存放该商品的售货器（以便将售货器中的商品数量减 1 并显示商品价格）以及收银机（以便更新现金）。因此，该函数有两个参数：一个对应售货器，另一个对应收银机。此外，两个参数都必须是引用参数。

用伪代码表示，该函数的算法是：

- 1. 如果售货器不为空，
  - a. 显示并提示顾客输入商品价格。
  - b. 获取顾客输入的金额。
  - c. 如果顾客输入的金额小于商品价格，
    - i. 显示并提示顾客输入追加金额。
    - ii. 计算顾客输入的总金额。
  - d. 如果顾客输入的金额至少等于商品价格，
    - i. 更新收银机中的金额。
    - ii. 售出商品——也就是说，将售货器中的商品数量减 1。
    - iii. 显示相应消息。
  - e. 如果用户输入的金额小于商品价格，则退还该金额。
- 2. 如果售货器为空，则告诉用户该商品已售罄。

函数 `sellProduct` 的定义如下：

```cpp
void sellProduct(dispenserType& product,
                cashRegister& pCounter)
{
    int amount;  //variable to hold the amount entered
    int amount2; //variable to hold the extra amount needed

    if (product.getNoOfItems() > 0) //if the dispenser is not
                                    //empty
    {
        cout << "Please deposit " << product.getCost()
             << " cents" << endl;
        cin >> amount;
```

```cpp
/**************************************************************
// Author: D.S. Malik
//
// class cashRegister
// This class specifies the members to implement a cash
// register.
//**************************************************************

class cashRegister
{
public:
    int getCurrentBalance() const;
        //Function to show the current amount in the cash
        //register.
        //Postcondition: The value of cashOnHand is returned.

    void acceptAmount(int amountIn);
        //Function to receive the amount deposited by
        //the customer and update the amount in the register.
        //Postcondition: cashOnHand = cashOnHand + amountIn;

    cashRegister(int cashIn = 500);
        //Constructor
        //Sets the cash in the register to a specific amount.
        //Postcondition: cashOnHand = cashIn;
        //             If no value is specified when the
        //             object is declared, the default value
        //             assigned to cashOnHand is 500.

private:
    int cashOnHand;    //variable to store the cash
                       //in the register
};

/**************************************************************
// Author: D.S. Malik
//
// class dispenserType
// This class specifies the members to implement a dispenser.
//**************************************************************

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
```

