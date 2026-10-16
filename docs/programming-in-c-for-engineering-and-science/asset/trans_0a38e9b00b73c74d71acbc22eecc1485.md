

# 示例 10.3 找零分配器

```
/* This driver program tests function makeChange().

   Input:  the cost of an item, and the amount paid
   Output: the change in terms of numbers of dollars, quarters,
           dimes, nickels, and pennies
---------------------------------------------------------------------*/

#include <iostream>      // cout, cin, <<, >>
#include <string>        // string
using namespace std;

void makeChange(double purchaseAmount, double payment,
                int & dollars, int & quarters, int & dimes,
                int & nickels, int & pennies);

int main()
{
    cout << "This program tests a change-making function...\n\n";

    double itemCost,      // a purchase
           amountPaid;    // what was paid
    int numDollars,        // variables for
        numQuarters,       // the values
        numDimes,          // to be output
        numNickels,
        numPennies;

    for (;;)
    {
        cout << "Enter item cost (negative to quit) and amount paid: ";
        cin >> itemCost;
        if (itemCost < 0) break;
        cin >> amountPaid;

        makeChange(itemCost, amountPaid, numDollars,
                   numQuarters,numDimes, numNickels, numPennies);

        cout << "The change from this purchase is:\n"
             << numDollars << " dollars,\n"
             << numQuarters << " quarters,\n"
             << numDimes << " dimes,\n"
             << numNickels << " nickels, and\n"
             << numPennies << " pennies\n\n";
    }
}
```

```
/* Function to compute the dollars, quarters, dimes, nickels, and pennies in change given the amount of a purchase and the amount paid.

Receive:      purchaseAmount, the (real) amount of the purchase,
              payment, the (real) amount of the payment
Precondition: purchaseAmount <= payment.
Pass back:    dollars, the (integer) number of dollars,
              quarters, the (integer) number of quarters,
              dimes, the (integer) number of dimes,
              nickels, the (integer) number of nickels, and
              pennies, the (integer) number of pennies in change
-------------------------------------------------------------------*/

void makeChange(double purchaseAmount,  // amount of purchase
                double payment,         // amount of payment
                int & dollars,          // dollars of change
                int & quarters,         // quarters of change
                int & dimes,            // dimes of change
                int & nickels,          // nickels of change
                int & pennies)          // pennies of change
{
    int change = int(100.0 * (payment - purchaseAmount) + 0.5);
    if (change > 0)
    {
        dollars = change / 100;   // 100 pennies per dollar
        change %= 100;            // compute remaining change

        quarters = change / 25;   // 25 pennies per quarter
        change %= 25;             // compute remaining change

        dimes = change / 10;      // 10 pennies per dime
        change %= 10;             // compute remaining change

        nickels = change / 5;     // 5 pennies per nickel
        pennies = change % 5;     // pennies are all that's left
    }
    else
    {
        cerr << "*** Purchase amount: " << purchaseAmount
             << " exceeds payment: " << payment << endl;
        dollars = quarters = dimes = nickels = pennies = 0;
    }
}
```

# 示例运行：

This program tests a change-making function...

Enter item cost (negative to quit) and amount paid: 1.01 2.00

The change from this purchase is:
0 dollars,
3 quarters,
2 dimes,
0 nickels, and
4 pennies

```
Enter item cost (negative to quit) and amount paid: 1.34 5.00
The change from this purchase is:
3 dollars,
2 quarters,
1 dimes,
1 nickels, and
1 pennies
```

```
Enter item cost (negative to quit) and amount paid: 1.05 1.00
*** Purchase amount: 1.05 exceeds payment: 1
The change from this purchase is:
0 dollars,
0 quarters,
0 dimes,
0 nickels, and
0 pennies
```

```
Enter item cost (negative to quit) and amount paid: -1 -1
```

## 10.3.2 示例 2：交换两个变量的值

在某些问题中，需要交换两个变量的值。在这里，我们将通过构造一个函数 `swap()` 来说明如何做到这一点，以便函数调用

```
swap(var1, var2);
```

会交换变量 *var1* 和 *var2* 的值。

我们的函数将有两个参数，我们将它们命名为 *first* 和 *second*。由于 *first* 的值必须改为 *second* 的值，因此 *second* 必须被函数接收，而 *first* 必须传回，并且由于 *second* 的值必须改为 *first* 的值，因此 *first* 必须被接收而 *second* 传回。因此，两个参数都具有 *in-out* 传参方式，并且可以应用规则 P4，将 *first* 和 *second* 作为引用参数，因为它们既被传回也被接收。

下面显示了此类函数的模式。

```
/* Function to interchange the values of two variables.

   Receive:   values of variables first and second
   Pass back: first, containing the value of second, and second,
              containing the value of first
------------------------------------------------------------*/
```

```
void swap(____ & first, ____ & second)
{
    ____ temporary = first;
    first = second;
    second = temporary;
}
```

用要交换的变量的类型替换空白，将产生一个可并入程序中在需要交换值时使用的 C++ 函数。示例 10.4 中的简单程序对此进行了说明，针对的是 int 变量。 （在第 10.5 节中，我们将看到如何让编译器自动执行这种“填空”。）

## 示例 10.4 交换两个 int 变量的值

```
/* Test driver for the swap() function

    Input: two integer values stored in intVar1 and intVar2
    Output: the values of intVar1 and intVar2 after swapping
    --------------------------------------------------------------*/

#include <iostream>
using namespace std;

void swap(int & first, int & second);

int main()
{
    int intVar1, intVar2;

    cout << "Enter two integers: ";
    cin >> intVar1 >> intVar2;

    swap(intVar1, intVar2);

    cout << "After using swap(), values are "
         << intVar1 << " and " << intVar2 << endl;
}
```

```
/* Function to interchange the values of two variables.

    Receive: values of int variables first and second
    Pass back: first, containing the value of second, and second,
               containing the value of first
    --------------------------------------------------------------*/

void swap(int & first, int & second)
{
    int temporary = first;
    first = second;
    second = temporary;
}
```

# 示例运行：

Enter two integers: 123 456789
After using swap(), values are 456789 and 123

## 10.3.3 示例 3：处理 IP 地址

在第 7.1 节中，我们考虑了 IP 地址，它们用于唯一标识连接到互联网的设备。每个这样的地址由四个字段组成，表示互联网的特定部分

host.subdomain.subdomain.rootdomain

计算机将其翻译为唯一的数字地址。我们开发了一个程序（参见示例 7.1）来将 IP 地址拆分为其四个组成部分。我们可以通过将其打包成如示例 10.5 所示的函数，使其在其他程序中易于重用。

## 示例 10.5 处理 IP 地址

```
/* This program uses a function to find the four network/host information blocks in an IP address.

Input: IP addresses
Output: four network/host information blocks, or an error message
---------------------------------------------------------------*/

#include <iostream>          // cin, cout
#include <string>            // string class
#include <cassert>           // assert()
using namespace std;

void chopIPAddress(const string & address, string & block1, string &
                   block2, string & block3, string & block4);

int main()
{
    string address, block1, block2, block3, block4;

    for(;;)
    {
        cout << "\nEnter an IP address (STOP to quit): ";
        cin >> address;
```

