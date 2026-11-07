

```cpp
//************************************************************
// Author: D.S. Malik
//
// class cashRegister
// This class specifies the members to implement a cash
// register.
//************************************************************

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
    int cashOnHand;    //variable to store the cash
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
        //
        //              If no value is specified for a
        //              parameter, then its default value is
        //              assigned to the corresponding member
        //              variable.
        //
private:
    int numberOfItems;       //variable to store the number of
                             //items in the dispenser
    int cost;  //variable to store the cost of an item
};

//*******************************************************
// Author: D.S. Malik
//
// Implementation file candyMachineImp.cpp
// This file contains the definitions of the functions to
// implement the operations of the classes cashRegister and
// dispenserType.
//*******************************************************

#include <iostream>
#include "candyMachine.h"

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
```

```cpp
{
    case 1:
        sellProduct(candy, counter);
        break;
    case 2:
        sellProduct(chips, counter);
        break;
    case 3:
        sellProduct(gum, counter);
        break;
    case 4:
        sellProduct(cookies, counter);
        break;
    default:
        cout << "Invalid selection." << endl;
    }//end switch
    showSelection();
    cin >> choice;
}//end while

    return 0;
}//end main

void showSelection()
{
    cout << "*** Welcome to Shelly's Candy Shop ***" << endl;
    cout << "To select an item, enter " << endl;
    cout << "1 for Candy" << endl;
    cout << "2 for Chips" << endl;
    cout << "3 for Gum" << endl;
    cout << "4 for Cookies" << endl;
    cout << "type " << "9 to exit" << endl;
}//end showSelection

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
                 << "enjoy." << endl;
        }
        else
            cout << "The amount is not enough. "
                 << "Collect what you deposited." << endl;

        cout << "*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*"
             << endl << endl;
    }
    else
        cout << "Sorry, this item is sold out." << endl;
}//end sellProduct
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```text
*** Welcome to Shelly's Candy Shop ***
To select an item, enter
1 for Candy
2 for Chips
3 for Gum
4 for Cookies
9 to exit
1
Please deposit 50 cents
50
Collect your item at the bottom and enjoy.
*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*

*** Welcome to Shelly's Candy Shop ***
To select an item, enter
1 for Candy
2 for Chips
3 for Gum
4 for Cookies
9 to exit
9
```

> **注意** 我们将类 `cashRegister` 和 `dispenserType` 的定义放在同一个头文件 `candyMachine.h` 中。但是，你也可以将这些类的定义放在单独的头文件中，并在使用这些类的文件中包含这些头文件，例如这些类的实现文件以及包含主程序的文件。同样，你也可以为这些类创建单独的实现文件。本书附带的网站包含这些头文件和实现文件。

## 快速回顾

- 1. `class` 是固定数量组件的集合。
- 2. `class` 的组件称为类的成员。
- 3. 类的成员通过名称访问。
- 4. 在 C++ 中，`class` 是保留字。
- 5. 类的成员分为三类之一：`private`、`protected` 和 `public`。
- 6. 类的 `private` 成员不能在类外部访问。
- 7. 类的 `public` 成员可以在类外部访问。
- 8. 默认情况下，类的所有成员都是 `private`。
- 9. `public` 成员使用成员访问说明符 `public` 和冒号 `:` 声明。
- 10. `private` 成员使用成员访问说明符 `private` 和冒号 `:` 声明。
- 11. 类的成员可以是函数或变量。
- 12. 如果类的任何成员是函数，通常使用函数原型来声明它。
- 13. 如果类的任何成员是变量，则像声明任何其他变量一样声明它。
- 14. 在类的定义中，声明变量时不能初始化它。
- 15. 在类的统一建模语言（UML）图中，顶部框包含类名。中间框包含成员变量及其数据类型。最后一个框包含成员函数名、参数列表和函数的返回类型。成员前面的 +（加号）表示该成员是 `public` 成员。成员前面的 −（减号）表示这是 `private` 成员。成员名前的 # 符号表示该成员是 `protected` 成员。
- 16. 在 C++ 中，`class` 是一种定义。不会为 `class` 本身分配内存；当你声明类变量时，才会为类变量分配内存。
- 17. 在 C++ 中，类变量称为类对象、类实例，或简称为对象。
- 18. 类成员通过类变量名、后跟点运算符（`.`）、再后跟成员名来访问。
- 19. 对类的唯一内置操作是赋值和成员选择。
- 20. 作为函数参数，类可以按值传递或按引用传递。
- 21. 函数可以返回 `class` 类型的值。
- 22. 任何使用类的程序（或软件）都称为该类的客户端。

