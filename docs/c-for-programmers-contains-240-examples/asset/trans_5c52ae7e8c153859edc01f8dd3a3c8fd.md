

## Performance Tip 6.9

避免在性能关键情况下使用递归。递归调用会花费时间并消耗额外的内存。

## Common Programming Error 6.26

意外地让一个非递归函数调用自身，无论是直接还是间接地通过另一个函数，都是逻辑错误。

## 6.22 （可选）软件工程案例研究：在 ATM 系统中识别类操作

在第 3 章、第 4 章和第 5 章末尾的软件工程案例研究部分，我们对 ATM 系统进行了面向对象设计的最初几个步骤。在第 3 章中，我们确定了需要实现 的类并创建了第一个类图。在第 4 章中，我们描述了一些类的属性。在第 5 章中，我们检查了对象状态并对对象状态转换和活动进行了建模。现在，我们确定实现 ATM 系统所需的某些类操作（或行为）。

### Identifying Operations

操作是类的对象为该类的客户端提供的服务。考虑一些现实世界对象的操作。收音机的操作包括设置其电台和音量（通常由人调节收音机的控件来调用）。汽车的操作包括加速（由驾驶员踩下油门踏板调用）、减速（由驾驶员踩下刹车踏板或松开油门踏板调用）、转弯和换挡。软件对象也可以提供操作——例如，一个软件图形对象可能提供绘制圆、绘制线、绘制正方形等操作。电子表格软件对象可能提供打印电子表格、对行或列中的元素求和以及将电子表格中的信息作为条形图或饼图绘制等操作。

我们可以通过检查需求规范中的关键动词和动词短语来推导出每个类的许多操作。然后我们将这些与系统中特定的类相关联（图 6.32）。图 6.32 中的动词短语帮助我们确定每个类的操作。

| Class | Verbs and verb phrases |
| --- | --- |
| ATM | executes financial transactions |
| BalanceInquiry | [none in the requirements specification] |
| Withdrawal | [none in the requirements specification] |
| Deposit | [none in the requirements specification] |
| BankDatabase | authenticates a user, retrieves an account balance, credits a deposit amount to an account, debits a withdrawal amount from an account |
| Account | retrieves an account balance, credits a deposit amount to an account, debits a withdrawal amount from an account |
| Screen | displays a message to the user |
| Keypad | receives numeric input from the user |
| CashDispenser | dispenses cash, indicates whether it contains enough cash to satisfy a withdrawal request |
| DepositSlot | receives a deposit envelope |

Fig. 6.32 | Verbs and verb phrases for each class in the ATM system. (Part 1 of 2.)
Fig. 6.32 | Verbs and verb phrases for each class in the ATM system. (Part 2 of 2.)

### Modeling Operations

要创建图 6.33 的更新类图，我们首先通过检查图 6.32 中为每个类列出的动词短语来识别操作。与类 ATM 关联的“executes financial transactions”短语意味着类 ATM 指示交易执行。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_265_0.png)

Fig. 6.33 | Classes in the ATM system with attributes and operations.

因此，类 BalanceInquiry、Withdrawal 和 Deposit 各自需要一个操作来向 ATM 提供此服务。我们将此操作（我们将其命名为 execute）放在图 6.33 的类图中三个交易类的第三个隔间中。在一次 ATM 会话期间，ATM 对象将调用每个交易对象的 execute 操作来告诉它执行。

UML 通过列出操作名，后跟括号中的以逗号分隔的参数列表、冒号和返回类型来表示操作（在 C++ 中实现为成员函数）：

```
operationName( parameter1, parameter2, ..., parameterN ) : return type
```

以逗号分隔的参数列表中的每个参数由参数名、冒号和参数类型组成：

```
parameterName : parameterType
```

目前，我们不列出操作的参数——我们稍后会识别并建模某些操作的参数。对于某些操作，我们尚不知道返回类型，因此我们也将其从图中省略。这种省略在此阶段是完全正常的。随着设计和实现的进行，我们将添加剩余的返回类型。

### Operations of Class BankDatabase and Class Account

图 6.32 在类 BankDatabase 旁边列出了短语“authenticates a user”——数据库是包含确定用户输入的账号和 PIN 是否与银行持有的账号匹配所需的账户信息的对象。因此，类 BankDatabase 需要一个操作来向 ATM 提供身份验证服务。我们将操作 authenticateUser 放在类 BankDatabase 的第三个隔间中（图 6.33）。然而，类 Account 的对象，而不是类 BankDatabase 的对象，存储了必须访问以验证用户的账号和 PIN，因此类 Account 必须提供一项服务来验证通过用户输入获得的 PIN 与 Account 对象中存储的 PIN 是否匹配。因此，我们向类 Account 添加一个 validatePIN 操作。请注意，我们为 authenticateUser 和 validatePIN 操作指定了 Boolean 的返回类型。每个操作返回一个值，指示操作是否成功执行其任务（即返回值为 true）或未成功（即返回值为 false）。

图 6.32 为类 BankDatabase 列出了几个额外的动词短语：“retrieves an account balance”、“credits a deposit amount to an account” 和 “debits a withdrawal amount from an account”。与“authenticates a user”一样，这些剩余的短语指的是数据库必须向 ATM 提供的服务，因为数据库保存了用于验证用户和执行 ATM 交易的所有账户数据。然而，类 Account 的对象实际上执行与这些短语相关的操作。因此，我们为类 BankDatabase 和类 Account 分别分配一个与这些短语对应的操作。回想一下第 3.11 节，由于银行账户包含敏感信息，我们不允许 ATM 直接访问账户。数据库充当 ATM 与账户数据之间的中介，从而防止未经授权的访问。正如我们在第 7.12 节中看到的，类 ATM 调用类 BankDatabase 的操作，每个操作又调用类 Account 中同名的操作。

短语“retrieves an account balance” 表明类 BankDatabase 和类 Account 各自需要一个 getBalance 操作。然而，请记住，我们在类 Account 中创建了两个属性来表示余额——availableBalance 和 totalBalance。余额查询需要访问这两个余额属性，以便将其显示给用户，但取款只需要检查 availableBalance 的值。为了允许系统中的对象单独获取每个余额属性，我们向类 BankDatabase 和类 Account 的第三个隔间添加了操作 getAvailableBalance 和 getTotalBalance（图 6.33）。我们为每个操作指定 Double 的返回类型，因为它们检索的余额属性的类型为 Double。

短语“credits a deposit amount to an account” 和 “debits a withdrawal amount from an account” 表明类 BankDatabase 和类 Account 必须在存款和取款期间分别执行更新账户的操作。因此，我们为类 BankDatabase 和类 Account 分配 credit 和 debit 操作。你可能记得，记入账户（例如存款）仅将金额添加到 totalBalance 属性。相反，借记账户（例如取款）会从两个余额属性中减去该金额。我们将这些实现细节隐藏在类 Account 内部。这是一个封装和信息隐藏的良好示例。

如果这是一个真正的 ATM 系统，类 BankDatabase 和类 Account 还将提供一组操作，允许另一个银行系统在确认或拒绝全部或部分存款后更新用户的账户余额。例如，操作 confirmDepositAmount 将向 availableBalance 属性添加一个金额，从而使存款资金可供取款。操作 rejectDepositAmount 将从 totalBalance 属性中减去一个金额，以指示最近通过 ATM 存款并添加到 totalBalance 的指定金额未在存款信封中找到。银行在确定用户未包含正确的现金金额或任何支票未兑现（即“跳票”）后会调用此操作。虽然添加这些操作会使我们的系统更完整，但我们并未将其包含在我们的类图中或我们的实现中，因为它们超出了案例研究的范围。

### Operations of Class Screen

类 Screen 在 ATM 会话的各个时间点“displays a message to the user”。所有视觉输出都通过 ATM 的屏幕进行。需求规范描述了屏幕向用户显示的许多类型的消息（例如欢迎消息、错误消息、感谢消息）。需求规范还指出屏幕向用户显示提示和菜单。然而，提示实际上只是描述用户接下来应输入内容的 消息，而菜单本质上是一种由一系列连续显示的消息（即菜单选项）组成的提示。因此，而不是为类 Screen 分配单独的操作来显示每种类型的消息、提示和菜单，我们只需创建一个可以显示由参数指定的任何消息的操作。我们将此操作（displayMessage）放在我们的类图中类 Screen 的第三个隔间中（图 6.33）。请注意，我们目前不担心此操作的 参数——我们稍后在本节中对参数进行建模。

### Operations of Class Keypad

从图 6.32 中类 Keypad 列出的短语“receives numeric input from the user” 中，我们得出结论，类 Keypad 应执行 getInput 操作。因为 ATM 的

