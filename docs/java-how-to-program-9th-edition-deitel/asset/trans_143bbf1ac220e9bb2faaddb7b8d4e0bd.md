
// Deposit.java
// Represents a deposit ATM transaction

public class Deposit extends Transaction
{
    private double amount; // amount to deposit
    private Keypad keypad; // reference to keypad
    private DepositSlot depositSlot; // reference to deposit slot
    private final static int CANCELED = 0; // constant for cancel option

    // Deposit constructor
    public Deposit( int userAccountNumber, Screen atmScreen,
        BankDatabase atmBankDatabase, Keypad atmKeypad,
        DepositSlot atmDepositSlot )
    {
        // initialize superclass variables
        super( userAccountNumber, atmScreen, atmBankDatabase );

        // initialize references to keypad and deposit slot
        keypad = atmKeypad;
        depositSlot = atmDepositSlot;
    } // end Deposit constructor

    // perform transaction
    @Override
    public void execute()
    {
        BankDatabase bankDatabase = getBankDatabase(); // get reference
        Screen screen = getScreen(); // get reference

        amount = promptForDepositAmount(); // get deposit amount from user

        // check whether user entered a deposit amount or canceled
        if ( amount != CANCELED )
        {
            // request deposit envelope containing specified amount
            screen.displayMessage(
                "\nPlease insert a deposit envelope containing " );
            screen.displayDollarAmount( amount );
            screen.displayMessageLine( "." );

            // receive deposit envelope
            boolean envelopeReceived = depositSlot.isEnvelopeReceived();

            // check whether deposit envelope was received
            if ( envelopeReceived )
            {
                screen.displayMessageLine( "\nYour envelope has been " +
                    "received.\nNOTE: The money just deposited will not " +
                    "be available until we verify the amount of any " +
                    "enclosed cash and your checks clear." );
                // credit account to reflect the deposit
                bankDatabase.credit( getAccountNumber(), amount );
            } // end if
            else // deposit envelope not received
            {
                screen.displayMessageLine( "\nYou did not insert an " +
                    "envelope, so the ATM has canceled your transaction." );
            } // end else
        } // end if
        else // user canceled instead of entering amount
        {
            screen.displayMessageLine( "\nCanceling transaction..." );
        } // end else
    } // end method execute

    // prompt user to enter a deposit amount in cents
    private double promptForDepositAmount()
    {
        Screen screen = getScreen(); // get reference to screen

        // display the prompt
        screen.displayMessage( "\nPlease enter a deposit amount in " +
            "CENTS (or 0 to cancel): " );
        int input = keypad.getInput(); // receive input of deposit amount

        // check whether the user canceled or entered a valid amount
        if ( input == CANCELED )
            return CANCELED;
        else
        {
            return ( double ) input / 100; // return dollar amount
        } // end else
    } // end method promptForDepositAmount
} // end class Deposit

## Fig. 13.23 | Class Deposit represents a deposit ATM transaction. (Part 2 of 2.)

与 Withdrawal 类似，类 Deposit 包含一个构造函数（第 12–22 行），它将三个参数传递给超类 Transaction 的构造函数。该构造函数还具有参数 atmKeypad 和 atmDepositSlot，并将其分配给对应的属性（第 20–21 行）。

方法 execute（第 25–66 行）重写了超类 Transaction 中的抽象版本，并提供了一个具体的实现来执行存款交易所需的步骤。第 28–29 行获取数据库和屏幕的引用。第 31 行通过调用私有实用方法 promptForDepositAmount（声明于第 69–85 行）提示用户输入存款金额，并将属性 amount 设置为返回的值。方法 promptForDepositAmount 要求用户以整数分的形式输入存款金额（因为 ATM 的键盘不包含小数点；这与许多真实 ATM 一致），并返回表示应存款美元金额的 double 值。

方法 promptForDepositAmount 中的第 71 行获取对 ATM 屏幕的引用。第 74–75 行显示一条消息，要求用户以分为单位输入存款金额，或输入“0”以取消交易。第 76 行从键盘接收用户的输入。第 79–84 行判断用户是否输入了真实的存款金额或选择取消。如果是后者，第 80 行返回常量 CANCELED。否则，第 83 行在将输入转换为 double 后除以 100，从而将存款金额从分为单位转换为美元金额。例如，如果用户输入 125 表示分为单位，第 83 行返回 125.0 除以 100，即 1.25——125 分等于 1.25 美元。

方法 execute 中的第 34–65 行判断用户是否选择取消交易而不是输入存款金额。如果用户取消，第 64 行显示相应的消息，然后方法返回。如果用户输入存款金额，第 37–40 行指示用户插入包含正确金额的存款信封。回想一下，Screen 方法 displayDollarAmount 会将 double 格式化为美元金额输出。

第 43 行将局部布尔变量设置为 depositSlot 的 isEnvelopeReceived 方法返回的值，表示是否已收到存款信封。回想一下，我们编写的 isEnvelopeReceived 方法（图 13.17 的第 8–11 行）始终返回 true，因为我们模拟存款槽的功能并假设用户总是插入信封。然而，我们编写类 Deposit 的 execute 方法以测试用户未插入信封的可能性——良好的软件工程要求程序考虑所有可能的返回值。因此，类 Deposit 已为 isEnvelopeReceived 的未来版本做好准备，该版本可能返回 false。如果存款槽收到信封，则执行第 48–54 行。第 48–51 行向用户显示适当的消息。第 54 行随后将存款金额记入用户在数据库中的账户。如果存款槽未收到存款信封，则执行第 58–59 行。在这种情况下，我们向用户显示一条消息，说明 ATM 已取消交易。随后方法返回，且不会修改用户的账户。

## 13.4.12 Class ATMCaseStudy

类 ATMCaseStudy（图 13.24）是一个简单的类，允许我们启动或“打开”ATM 并测试 ATM 系统模型的实现。类 ATMCaseStudy 的 main 方法（第 7–11 行）除了实例化一个名为 theATM 的新 ATM 对象（第 9 行）并调用其 run 方法（第 10 行）以启动 ATM 之外，没有做其他事情。

```
// ATMCaseStudy.java
// Driver program for the ATM case study

public class ATMCaseStudy
{
    // main method creates and runs the ATM
    public static void main( String[] args )
    {
        ATM theATM = new ATM();
        theATM.run();
    } // end main
} // end class ATMCaseStudy
```

Fig. 13.24 | ATMCaseStudy.java starts the ATM.

## 13.5 Wrap-Up

在本章中，你使用继承来调整 ATM 软件系统的设计，并在 Java 中完全实现了 ATM。恭喜你完成了整个 ATM 案例研究！我们希望你觉得这次经历很有价值，并且它强化了你所学到的许多面向对象编程概念。在下一章中，我们将更深入地探讨图形用户界面（GUI）。

## Answers to Self-Review Exercises

13.1 True. The minus sign (–) indicates private visibility.

13.2 b.

13.3 The design for class Keypad yields the code in Fig. 13.25. Recall that class Keypad has no attributes for the moment, but attributes may become apparent as we continue the implementation. Also, if we were designing a real ATM, method getInput would need to interact with the ATM’s keypad hardware. We’ll actually read input from the keyboard of a personal computer when we write the complete Java code in Section 13.4.

```
// Class Keypad represents an ATM’s keypad
public class Keypad
{
    // no attributes have been specified yet
    // no-argument constructor
    public Keypad()
    {
    } // end no-argument Keypad constructor
    // operations
    public int getInput()
    {
    } // end method getInput
} // end class Keypad
```

Fig. 13.25 | Java code for class Keypad based on Figs. 13.1–13.2.

13.4 b.

13.5 False. The UML requires that we italicize abstract class names and method names.

13.6 The design for class Transaction yields the code in Fig. 13.26. The bodies of the class constructor and methods are completed in Section 13.4. When fully implemented, methods getScreen and getBankDatabase will return superclass Transaction’s private reference attributes screen and bankDatabase, respectively. These methods allow the Transaction subclasses to access the ATM’s screen and interact with the bank’s database.

```
// Abstract class Transaction represents an ATM transaction
public abstract class Transaction
{
    // attributes
    private int accountNumber; // indicates account involved
    private Screen screen; // ATM’s screen
    private BankDatabase bankDatabase; // account info database
```

Fig. 13.26 | Java code for class Transaction based on Figs. 13.9 and 13.10. (Part 1 of 2.)

