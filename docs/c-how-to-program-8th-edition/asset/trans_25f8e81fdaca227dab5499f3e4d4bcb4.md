
```cpp
cashDispensed = true; // cash was dispensed

// instruct user to take cash
screen.displayMessageLine(
    "\nPlease take your cash from the cash dispenser.");
} // end if
else // cash dispenser does not have enough cash
screen.displayMessageLine(
    "\n\nInsufficient cash available in the ATM."
    "\n\nPlease choose a smaller amount.");
} // end if
else // not enough money available in user's account
{
    screen.displayMessageLine(
        "\nInsufficient funds in your account."
        "\n\nPlease choose a smaller amount.");
} // end else
} // end if
else // user chose cancel menu option
{
    screen.displayMessageLine( "\nCancelling transaction..." );
    transactionCanceled = true; // user canceled the transaction
} // end else
} while ( !cashDispensed && !transactionCanceled ); // end do...while
} // end function execution

// display a menu of withdrawal amounts and the option to cancel;
// return the chosen amount or 0 if the user chooses to cancel
int Withdrawal::displayMenuOfAmounts() const
{
    int userChoice = 0; // local variable to store return value

    Screen &screen = getScreen(); // get screen reference

    // array of amounts to correspond to menu numbers
    int amounts[] = { 0, 20, 40, 60, 100, 200 };

    // loop while no valid choice has been made
    while ( userChoice == 0 )
    {
        // display the menu
        screen.displayMessageLine( "\nWithdrawal options:" );
        screen.displayMessageLine( "1 - $20" );
        screen.displayMessageLine( "2 - $40" );
        screen.displayMessageLine( "3 - $60" );
        screen.displayMessageLine( "4 - $100" );
        screen.displayMessageLine( "5 - $200" );
        screen.displayMessageLine( "6 - Cancel transaction" );
        screen.displayMessage( "\nChoose a withdrawal option (1-6): " );

        int input = keypad.getInput(); // get user input through keypad

        // determine how to proceed based on the input value
        switch ( input )
        {
            case 1: // if the user chose a withdrawal amount
            case 2: // (i.e., chose option 1, 2, 3, 4 or 5), return the
            case 3: // corresponding amount from amounts array
            case 4:
            case 5:
                userChoice = amounts[ input ]; // save user's choice
                break;
            case CANCELED: // the user chose to cancel
                userChoice = CANCELED; // save user's choice
                break;
            default: // the user did not enter a value from 1-6
                screen.displayMessageLine(
                    "\nInvalid selection. Try again. ");
        } // end switch
    } // end while

    return userChoice; // return withdrawal amount or CANCELED
} // end function displayMenuOfAmounts
```

图 26.33 | Withdrawal 类成员函数定义。（第 3 部分，共 4 部分。）

图 26.33 | Withdrawal 类成员函数定义。（第 4 部分，共 4 部分。）

Withdrawal 类的构造函数（定义于图 26.33 第 13–20 行）有五个参数。它在第 16 行使用基类初始化器，将参数 userAccountNumber、atmScreen 和 atmBankDatabase 传递给基类 Transaction 的构造函数，以设置 Withdrawal 从 Transaction 继承的数据成员。该构造函数还接收引用 atmKeypad 和 atmCashDispenser 作为参数，并使用成员初始化器（第 17 行）将它们赋给引用数据成员 keypad 和 cashDispenser。

Withdrawal 类用具体实现（第 23–81 行）重写 Transaction 的纯虚函数 execute，该实现执行取款涉及的步骤。第 25 行声明并初始化一个局部 bool 变量 cashDispensed。该变量表示现金是否已发放（即交易是否已成功完成），初始值为 false。第 26 行声明一个 bool 变量 transactionCanceled 并将其初始化为 false，该变量表示交易是否已被用户取消。第 29–30 行通过调用继承自基类 Transaction 的成员函数，获得银行数据库和 ATM 屏幕的引用。

第 33–80 行包含一个 do...while 语句，该语句执行其循环体，直到现金被发放（即直到 cashDispensed 变为 true），或直到用户选择取消（即直到 transactionCanceled 变为 true）。如果发生错误（即请求的取款金额大于用户可用余额，或大于现金发放机中的现金金额），该循环会不断将用户带回交易开始处。第 36 行通过调用私有工具函数 displayMenuOfAmounts（定义于第 85–129 行）显示取款金额菜单并获取用户选择。该函数显示金额菜单，并返回一个 int 类型的取款金额，或返回 int 常量 CANCELED 以表示用户已选择取消交易。

成员函数 displayMenuOfAmounts（第 85–129 行）首先声明局部变量 userChoice（初始值为 0），用于存储该成员函数将返回的值（在第 87 行）。

## 26.4.1.1 Deposit 类

Deposit 类（图 26.34–26.35）派生自 Transaction，表示一笔 ATM 存款交易。图 26.34 包含 Deposit 类的定义。与派生类 BalanceInquiry 和 Withdrawal 一样，Deposit 声明了一个构造函数（第 13 行）和成员函数 execute（第 14 行）——我们稍后讨论这些内容。回想图 26.11 的类图，Deposit 类有一个属性 amount，第 16 行将其实现为 int 数据成员。第 17–18 行创建引用数据成员 keypad 和 depositSlot，用于实现图 26.10 中建模的 Deposit 类与 Keypad 类和 DepositSlot 类之间的关联。第 19 行包含私有工具函数 promptForDepositAmount 的函数原型，我们很快会讨论它。

```cpp
// Deposit.h
// Deposit class definition. Represents a deposit transaction.
#ifndef DEPOSIT_H
#define DEPOSIT_H

#include "Transaction.h" // Transaction class definition
class Keypad; // forward declaration of class Keypad
class DepositSlot; // forward declaration of class DepositSlot

class Deposit : public Transaction
{
public:
    Deposit( int, Screen &, BankDatabase &, Keypad &, DepositSlot & );
    virtual void execute(); // perform the transaction
private:
    double amount; // amount to deposit
    Keypad &keypad; // reference to ATM's keypad
    DepositSlot &depositSlot; // reference to ATM's deposit slot
    double promptForDepositAmount() const; // get deposit amount from user
}; // end class Deposit

#endif // DEPOSIT_H
```

图 26.34  |  Deposit 类定义。

### Deposit 类成员函数定义

图 26.35 给出 Deposit 类的实现。第 3 行通过 #include 包含 Deposit 类定义，第 4–7 行通过 #include 包含 Deposit 成员函数中使用的其他类的类定义。第 9 行声明一个常量 CANCELED，它对应于用户为取消存款而输入的值。我们现在讨论该类如何使用这个常量。

```cpp
// Deposit.cpp
// Member-function definitions for class Deposit.
#include "Deposit.h" // Deposit class definition
#include "Screen.h" // Screen class definition
#include "BankDatabase.h" // BankDatabase class definition
#include "Keypad.h" // Keypad class definition
#include "DepositSlot.h" // DepositSlot class definition

static const int CANCELED = 0; // constant representing cancel option

// Deposit constructor initializes class's data members
Deposit::Deposit( int userAccountNumber, Screen &atmScreen,
   BankDatabase &atmBankDatabase, Keypad &atmKeypad,
   DepositSlot &atmDepositSlot )
   : Transaction( userAccountNumber, atmScreen, atmBankDatabase ),
     keypad( atmKeypad ), depositSlot( atmDepositSlot )
{
   // empty body
} // end Deposit constructor

// performs transaction; overrides Transaction's pure virtual function
void Deposit::execute()
{
   BankDatabase &bankDatabase = getBankDatabase(); // get reference
   Screen &screen = getScreen(); // get reference

   amount = promptForDepositAmount(); // get deposit amount from user

   // check whether user entered a deposit amount or canceled
   if ( amount != CANCELED )
   {
      // request deposit envelope containing specified amount
      screen.displayMessage(
         "\nPlease insert a deposit envelope containing " );
      screen.displayDollarAmount( amount );
      screen.displayMessageLine( " in the deposit slot." );

      // receive deposit envelope
      bool envelopeReceived = depositSlot.isEnvelopeReceived();

      // check whether deposit envelope was received
      if ( envelopeReceived )
      {
         screen.displayMessageLine( "\nYour envelope has been received."
            "\nNOTE: The money deposited will not be available until we"
            "\nverify the amount of any enclosed cash, and any enclosed"
            "\nchecks clear." );

         // credit account to reflect the deposit
         bankDatabase.credit( getAccountNumber(), amount );
      } // end if
      else // deposit envelope not received
      {
         screen.displayMessageLine( "\nYou did not insert an "
            "envelope, so the ATM has canceled your transaction." );
      } // end else
   } // end if
   else // user canceled instead of entering amount
   {
```

图 26.35 | Deposit 类成员函数定义。（第 1 部分，共 3 部分。）

图 26.35 | Deposit 类成员函数定义。（第 2 部分，共 3 部分。）
