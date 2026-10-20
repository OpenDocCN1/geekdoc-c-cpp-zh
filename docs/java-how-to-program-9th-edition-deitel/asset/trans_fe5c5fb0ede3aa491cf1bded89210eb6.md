

```java
    // method overriding execute
    @Override
    public void execute()
    {
    } // end method execute
} // end class Withdrawal
```

图 13.12 | 基于图 13.9 和 13.10 的类 Withdrawal 的 Java 代码。（第 2 部分，共 2 部分。）

### 软件工程观察 13.2

 several UML 建模工具可以将基于 UML 的设计转换为 Java 代码，极大地加快了实现过程。如需了解这些工具的更多信息，请访问我们的 UML 资源中心 www.deitel.com/UML/。

恭喜你完成了案例研究的設計部分！我们在第 13.4 节用 Java 代码实现 ATM 系统。我们建议你仔细阅读代码及其说明。代码注释丰富，并且精确遵循你现在熟悉的设计。随附的说明经过精心编写，以指导你基于 UML 设计理解实现。掌握这段代码是在学习第 12.2–12.7 节和第 13.2–13.3 节后一个美妙的 culminating 成就。

### 第 13.3 节 自测练习

- 13.4 UML 使用带有 ________ 的箭头来表示泛化关系。
  - a) 实心箭头
  - b) 三角形空心箭头
  - c) 菱形空心箭头
  - d) 棒状箭头
- 13.5 判断以下陈述是否正确，如果错误，请说明原因：UML 要求我们下划线抽象类名和方法名。
- 13.6 编写 Java 代码以开始实现图 13.9 和 13.10 中指定的类 Transaction 的设计。确保包含基于类 Transaction 关联的私有引用类型属性。还应确保包含公共 get 方法，以提供对子类执行其任务所需的任何这些私有属性的访问。

## 13.4 ATM 案例研究实现

本节包含 ATM 系统完整的 673 行工作实现。我们按第 12.3 节中识别的顺序考虑类——ATM、Screen、Keypad、CashDispenser、DepositSlot、Account、BankDatabase、Transaction、BalanceInquiry、Withdrawal 和 Deposit。

我们应用第 13.2–13.3 节中讨论的准则，根据图 13.9 和 13.10 中的 UML 类图对这些类进行编码。为了开发类方法的主体，我们参考第 12.5 节中的活动图以及第 12.7 节中介绍的通信图和序列图。我们的 ATM 设计并未指定所有程序逻辑，也可能未指定完成 ATM 实现所需的所有属性和操作。这是面向对象设计过程的正常部分。随着我们实现系统，我们完成程序逻辑并在必要时添加属性和行为，以构建第 12.2 节需求文档中指定的 ATM 系统。

我们通过展示一个 Java 应用程序（ATMCaseStudy）来结束讨论，该应用程序启动 ATM 并使系统中的其他类投入使用。请记住，我们正在开发 ATM 系统的第一个版本，它运行在个人电脑上，并使用电脑的键盘和显示器来模拟 ATM 的键盘和屏幕。我们也仅模拟 ATM 的现金分配器和存款槽的动作。然而，我们尝试实现系统，以便这些设备的真实硬件版本可以在不进行重大代码更改的情况下集成。

### 13.4.1 类 ATM

类 ATM（图 13.13）代表整个 ATM。行 6–12 实现类的属性。我们从图 13.9 和 13.10 的 UML 类图中确定了除一个之外的所有这些属性。我们在图 13.10 中将 UML 布尔属性 userAuthenticated 实现为 Java 中的 boolean（第 6 行）。第 7 行声明了一个在 UML 设计中找不到的属性——一个 int 属性 currentAccountNumber，用于跟踪当前已认证用户的账号。我们很快就会看到类如何使用此属性。第 8–12 行声明了与图 13.9 中类图中建模的 ATM 类关联相对应的引用类型属性。这些属性允许 ATM 访问其部件（即其 Screen、Keypad、CashDispenser 和 DepositSlot）并与银行的账户信息数据库（即 BankDatabase 对象）交互。

```java
// ATM.java
// Represents an automated teller machine

public class ATM
{
    private boolean userAuthenticated; // whether user is authenticated
    private int currentAccountNumber; // current user's account number
    private Screen screen; // ATM's screen
    private Keypad keypad; // ATM's keypad
    private CashDispenser cashDispenser; // ATM's cash dispenser
    private DepositSlot depositSlot; // ATM's deposit slot
    private BankDatabase bankDatabase; // account information database

    // constants corresponding to main menu options
    private static final int BALANCE_INQUIRY = 1;
    private static final int WITHDRAWAL = 2;
    private static final int DEPOSIT = 3;
    private static final int EXIT = 4;

    // no-argument ATM constructor initializes instance variables
    public ATM()
    {
        userAuthenticated = false; // user is not authenticated to start
        currentAccountNumber = 0; // no current account number to start
        screen = new Screen(); // create screen
        keypad = new Keypad(); // create keypad
        cashDispenser = new CashDispenser(); // create cash dispenser
        depositSlot = new DepositSlot(); // create deposit slot
        bankDatabase = new BankDatabase(); // create acct info database
    } // end no-argument ATM constructor

    // start ATM
    public void run()
    {
        // welcome and authenticate user; perform transactions
        while ( true )
        {
            // loop while user is not yet authenticated
            while ( !userAuthenticated )
            {
                screen.displayMessageLine( "\nWelcome!" );
                authenticateUser(); // authenticate user
            } // end while

            performTransactions(); // user is now authenticated
            userAuthenticated = false; // reset before next ATM session
            currentAccountNumber = 0; // reset before next ATM session
            screen.displayMessageLine( "\nThank you! Goodbye!" );
        } // end while
    } // end method run

    // attempts to authenticate user against database
    private void authenticateUser()
    {
        screen.displayMessage( "\nPlease enter your account number: " );
        int accountNumber = keypad.getInput(); // input account number
        screen.displayMessage( "\nEnter your PIN: " ); // prompt for PIN
        int pin = keypad.getInput(); // input PIN

        // set userAuthenticated to boolean value returned by database
        userAuthenticated =
            bankDatabase.authenticateUser( accountNumber, pin );

        // check whether authentication succeeded
        if ( userAuthenticated )
        {
            currentAccountNumber = accountNumber; // save user's account #
        } // end if
        else
            screen.displayMessageLine(
                "Invalid account number or PIN. Please try again." );
    } // end method authenticateUser

    // display the main menu and perform transactions
    private void performTransactions()
    {
        // local variable to store transaction currently being processed
        Transaction currentTransaction = null;
        boolean userExited = false; // user has not chosen to exit

        // loop while user has not chosen option to exit system
        while ( !userExited )
        {
            // show main menu and get user selection
            int mainMenuSelection = displayMainMenu();

            // decide how to proceed based on user's menu selection
            switch ( mainMenuSelection )
            {
                // user chose to perform one of three transaction types
                case BALANCE_INQUIRY:
                case WITHDRAWAL:
                case DEPOSIT:

                    // initialize as new object of chosen type
                    currentTransaction =
                        createTransaction( mainMenuSelection );

                    currentTransaction.execute(); // execute transaction
                    break;
                case EXIT: // user chose to terminate session
                    screen.displayMessageLine( "\nExiting the system..." );
                    userExited = true; // this ATM session should end
                    break;
                default: // user did not enter an integer from 1-4
                    screen.displayMessageLine(
                        "\nYou did not enter a valid selection. Try again." );
                    break;
            } // end switch
        } // end while
    } // end method performTransactions

    // display the main menu and return an input selection
    private int displayMainMenu()
    {
        screen.displayMessageLine( "\nMain menu:" );
        screen.displayMessageLine( "1 - View my balance" );
        screen.displayMessageLine( "2 - Withdraw cash" );
        screen.displayMessageLine( "3 - Deposit funds" );
        screen.displayMessageLine( "4 - Exit\n" );
        screen.displayMessage( "Enter a choice: " );
        return keypad.getInput(); // return user's selection
    } // end method displayMainMenu

    // return object of specified Transaction subclass
    private Transaction createTransaction( int type )
    {
        Transaction temp = null; // temporary Transaction variable
```
