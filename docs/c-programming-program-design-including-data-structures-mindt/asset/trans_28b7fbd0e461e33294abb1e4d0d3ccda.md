
- d. 如果顾客输入的金额至少等于商品价格，
  - i. 通过加上用户输入的金额来更新收银机中的金额。
  - ii. 出售商品——也就是将分配器中的商品数量减 1。
  - iii. 显示相应的消息。
- e. 如果用户输入的金额小于商品价格，则退还该金额。
- 2. 如果分配器为空，则告诉用户该商品已售罄。

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
                 << "enjoy!" << endl;
        }
        else
            cout << "The amount is not enough."
                 << "Collect what you deposited." << endl;

        cout << "*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*"
             << endl << endl;
    }
    else
        cout << "Sorry, this item is sold out." << endl;
} //end sellProduct
```

既然我们已经描述了函数 **showSelection** 和 **sellProduct**，接下来描述函数 main。

## main

函数 main 的算法如下：

- 1. 创建收银机——也就是声明一个 **cashRegister** 类型的对象。
- 2. 创建四个分配器——也就是声明四个 **dispenserType** 类型的对象并初始化这些对象。例如，语句：

  ```cpp
  dispenserType orange(100, 50);
  ```

  创建了一个名为 orange 的分配器对象来盛放果汁。该分配器中的商品数量为 100，每件商品的价格为 50 美分。
- 3. 根据需要声明其他变量。
- 4. 显示选项；调用函数 **showSelection**。
- 5. 获取选择项。
- 6. 当未完成时（选择 9 会退出程序），
  - a. 出售商品；调用函数 **sellProduct**。
  - b. 显示选项；调用函数 **showSelection**。
  - c. 获取选择项。

函数 main 的定义如下：

```cpp
int main()
{
    cashRegister counter;
    dispenserType orange(100, 50);
    dispenserType apple(100, 65);
    dispenserType mango(75, 80);
    dispenserType strawberryBanana(100, 85);

    int choice;  //variable to hold the selection

    showSelection();
    cin >> choice;

    while (choice != 9)
    {
        switch (choice)
        {
        case 1:
            sellProduct(orange, counter);
            break;
        case 2:
            sellProduct(apple, counter);
            break;
        case 3:
            sellProduct(mango, counter);
            break;
        case 4:
            sellProduct(strawberryBanana, counter);
            break;
        default:
            cout << "Invalid selection." << endl;
        }//end switch

        showSelection();
        cin >> choice;
    }//end while

    return 0;
}//end main
```

## 完整程序清单

在前面的章节中，我们设计了用于实现收银机的类，以及用于实现果汁机的分配器。在本节中，为完整起见，我们给出这些类、实现文件以及用于实现果汁机的用户程序的完整定义。

```cpp
//***************************************************************
// Author: D. S. Malik
//
// class cashRegister
// This class specifies the members to implement a cash
// register.
//***************************************************************

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
        //              If no value is specified when the
        //              object is declared, the default value
        //              assigned to cashOnHand is 500.

private:
    int cashOnHand;        //variable to store the cash
                           //in the register
};

//************************************************************
// Author: D.S. Malik
//
// class dispenserType
// This class specifies the members to implement a dispenser.
//************************************************************

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
        //              parameter, then its default value is
        //              assigned to the corresponding member
        //              variable.

private:
    int numberOfItems;       //variable to store the number of
                             //items in the dispenser
    int cost;                //variable to store the cost of an item
};

//***************************************************************
// Author: D.S. Malik
//
// Implementation file juiceMachine.cpp
// This file contains the definitions of the functions to
// implement the operations of the classes cashRegister and
// dispenserType.
//***************************************************************

#include <iostream>
#include "juiceMachine.h"

using namespace std;

int cashRegister::getCurrentBalance() const
{
    return cashOnHand;
}

void cashRegister::acceptAmount(int amountIn)
{
    cashOnHand = cashOnHand + amountIn;
}

cashRegister::cashRegister(int cashIn)
{
    if (cashIn >= 0)
        cashOnHand = cashIn;
    else
        cashOnHand = 500;
}

int dispenserType::getNoOfItems() const
{
    return numberOfItems;
}

int dispenserType::getCost() const
{
    return cost;
}

void dispenserType::makeSale()
{
    numberOfItems--;
}

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

//***********************************************************
// Author: D.S. Malik
//
// This program uses the classes cashRegister and
// dispenserType to implement a juice machine.
//***********************************************************

#include <iostream>
#include "juiceMachine.h"

using namespace std;

void showSelection();
void sellProduct(dispenserType& product,
                 cashRegister& pCounter);

int main()
{
    cashRegister counter;
    dispenserType orange(100, 50);
    dispenserType apple(100, 65);
    dispenserType mango(75, 80);
    dispenserType strawberryBanana(100, 85);

    int choice;  //variable to hold the selection

    showSelection();
    cin >> choice;

    while (choice != 9)
    {
        switch (choice)
        {
        case 1:
            sellProduct(orange, counter);
            break;
```
