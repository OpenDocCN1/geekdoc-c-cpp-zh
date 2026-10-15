
// Fig. G.1: Account.h
// Definition of Account class.

class Account
{
public:
    Account( int ); // constructor initializes balance
    void credit( int ); // add an amount to the account balance
    void debit( int ); // subtract an amount from the account balance
    int getBalance(); // return the account balance
private:
    int balance; // data member that stores the balance
}; // end class Account

图 G.1 | Account 类的头文件。

// Fig. G.2: Account.cpp
// Member-function definitions for class Account.
#include <iostream>
using std::cout;
using std::endl;

#include "Account.h" // include definition of class Account

// Account constructor initializes data member balance
Account::Account( int initialBalance )
{
    balance = 0; // assume that the balance begins at 0

    // if initialBalance is greater than 0, set this value as the
    // balance of the account; otherwise, balance remains 0
    if ( initialBalance > 0 )
        balance = initialBalance;

    // if initialBalance is negative, print error message
    if ( initialBalance < 0 )
        cout << "Error: Initial balance cannot be negative.\n" << endl;
} // end Account constructor

// credit (add) an amount to the account balance
void Account::credit( int amount )
{
    balance = balance + amount; // add amount to balance
} // end function credit

// debit (subtract) an amount from the account balance
void Account::debit( int amount )
{
    if ( amount <= balance ) // debit amount does not exceed balance
        balance = balance - amount;

图 G.2 | Account 类的定义。（第 1 部分，共 2 部分）

```
36    else // debit amount does not exceed balance
37        cout << "Debit amount exceeded account balance.\n" << endl;
38    } // end function debit
39
40    // return the account balance
41    int Account::getBalance()
42    {
43        return balance; // gives the value of balance to the calling function
44    } // end function getBalance
```

图 G.2 | Account 类的定义。（第 2 部分，共 2 部分）

```
1  // Fig. G.3: figg_03.cpp
2  // Create and manipulate Account objects.
3  #include <iostream>
4  using std::cin;
5  using std::cout;
6  using std::endl;
7
8  // include definition of class Account from Account.h
9  #include "Account.h"
10
11  // function main begins program execution
12  int main()
13  {
14      Account account1( 50 ); // create Account object
15
16      // display initial balance of each object
17      cout << "account1 balance: $" << account1.getBalance() << endl;
18
19      int withdrawalAmount; // stores withdrawal amount read from user
20
21      cout << "\nEnter withdrawal amount for account1: "; // prompt
22      cin >> withdrawalAmount; // obtain user input
23      cout << "\nAttempting to subtract " << withdrawalAmount
24          << " from account1 balance\n\n";
25      account1.debit( withdrawalAmount ); // try to subtract from account1
26
27      // display balances
28      cout << "account1 balance: $" << account1.getBalance() << endl;
29      return 0; // indicate successful termination
30  } // end main
```

图 G.3 | 用于调试的测试类。

在以下步骤中，你将使用断点和各种调试器命令来检查图 G.3 中声明的变量 withdrawalAmount 的值。

+   1. 启用调试器。调试器通常默认已启用。如果尚未启用，你需要在工具栏中更改“解决方案配置”组合框（图 G.4）的设置。为此，请单击该组合框的下拉箭头，然后选择 Debug。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_986_0.png)

**图 G.4** | 启用调试器。

+   2. **_在 Visual Studio 中插入断点。_** 要在 Visual Studio 中插入断点，请单击要中断的代码行旁边的**_边距指示条_**（图 G.5 中代码窗口左侧的灰色边距），或右键单击该代码行并选择**断点 > 插入断点**。你可以根据需要设置任意数量的断点。请在代码的第 21 行和第 25 行设置断点。单击处会出现一个红色圆点，表示断点已设置（图 G.5）。程序运行时，调试器会在包含断点的任何行暂停执行。当调试器暂停程序时，称程序处于**_中断模式_**。断点可以在运行程序之前、中断模式中以及程序运行期间设置。

+   3. **_开始调试。_** 在代码编辑器中设置断点后，选择**生成 > 生成解决方案**编译程序，然后选择**调试 > 开始调试**开始调试过程。[_注意：_ 如果你没有先编译程序，选择**调试 > 开始调试**时它仍会被编译。] 调试控制台应用程序时，会出现一个**命令提示符**窗口（图 G.6），你可以在其中指定程序输入并查看程序输出。当执行到达第 21 行的断点时，调试器进入中断模式。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_986_1.png)

**图 G.5** | 设置两个断点。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_986_2.png)

**图 G.6** | 库存程序正在运行。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_988_0.png)

图 G.9 | 程序输出。

+   8. *禁用断点。* 要*禁用断点*，请右键单击已设置断点的代码行（或断点本身），然后选择**禁用断点**。已禁用的断点以空心圆表示（图 G.10）。禁用断点而不是删除断点，可以让你之后通过单击空心圆或右键单击空心圆并选择**启用断点**来重新启用该断点。

+   9. *删除断点。* 若要删除不再需要的断点，请右键单击已设置断点的代码行，然后选择**断点 > 删除断点**。你也可以通过单击边距指示条中的断点来删除断点。

+   10. *完成程序执行。* 选择**调试 > 继续**，使程序执行完毕。

在本节中，你学习了如何启用调试器和设置断点，以便在程序运行时检查代码结果。你还学习了如何在程序于断点处暂停执行后继续执行，以及如何禁用和删除断点。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_988_1.png)

图 G.10 | 已禁用的断点。

# G.3 局部变量窗口和监视窗口

在上一节中，你了解了*快速信息*功能允许你检查变量的值。在本节中，你将学习在程序运行时使用**局部变量窗口**为变量赋予新值。你还将使用**监视窗口**检查更复杂表达式的值。

+   1. *插入断点。* 清除现有断点。然后，单击源代码中第 25 行左侧的边距指示条，在第 25 行设置断点（图 G.11）。再单击第 28 行左侧的边距指示条，在第 28 行设置另一个断点。

+   2. **开始调试。** 选择**调试 > 开始**。在 **Enter withdrawal amount for account1:** 提示符处输入 13，然后按 *Enter*，让程序读取你刚输入的值。程序将一直执行到第 25 行的断点。

+   3. **暂停程序执行。** 调试器在第 25 行进入中断模式（图 G.12）。此时，第 22 行已输入你输入的 withdrawalAmount（13），第 23–24 行已输出程序将尝试取款的信息，第 25 行是接下来将要执行的语句。

+   4. **检查数据。** 在中断模式下，你可以使用调试器的**局部变量**窗口查看局部变量的值。要打开**局部变量**窗口，请选择**调试 > 窗口 > 局部变量**。图 G.13 显示了 `main` 的局部变量 `account1` 和 `withdrawalAmount`（13）的值。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_989_0.png)

**图 G.11** | 在第 25 行和第 28 行设置断点。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_989_1.png)

**图 G.12** | 调试器到达第 25 行断点时程序执行暂停。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_989_2.png)

**图 G.13** | 检查变量 `withdrawalAmount`。
