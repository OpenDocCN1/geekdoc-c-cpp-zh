
![](img/bfd978e7e9b192bab46ec2a89e481263_1147_0.png)

- 26.1 引言
- 26.2 开始为 ATM 系统的类编程
- 26.3 将继承融入 ATM 系统
- 26.4 ATM 案例研究实现
  - 26.4.1 ATM 类
  - 26.4.2 Screen 类
  - 26.4.3 Keypad 类
  - 26.4.4 CashDispenser 类
  - 26.4.5 DepositSlot 类
  - 26.4.6 Account 类
  - 26.4.7 BankDatabase 类
  - 26.4.8 Transaction 类
  - 26.4.9 BalanceInquiry 类
  - 26.4.10 Withdrawal 类
  - 26.4.11 Deposit 类
  - 26.4.12 Program ATMCaseStudy.cpp 类
- 26.5 总结

## 26.1 引言

在第25章中，我们为ATM系统开发了一个面向对象设计。现在开始用C++实现我们的面向对象设计。在26.2节中，我们展示如何将类图转换为C++代码。在26.3节中，我们用继承和多态来调整设计。然后在26.4节中给出ATM软件的完整C++代码实现。代码有仔细的注释，实现讨论详尽而准确。研究这个应用使你有机会看到一个更实质性的应用，这类应用你很可能在工业界遇到。

## 26.2 开始为 ATM 系统的类编程

> [注：本节可在第9章之后学习。]

### 可见性

现在我们对类的成员应用访问说明符。访问说明符`public`和`private`决定一个对象的属性和操作对其他对象的可见性或可访问性。在开始实现我们的设计之前，我们必须考虑类中哪些属性和操作应当是公有的，哪些应当是私有的。

前面我们观察到，数据成员通常应当是私有的，而由给定类的客户端调用的成员函数应当是公有的。然而，仅由该类的其他成员函数作为“实用函数”调用的成员函数通常应当是私有的。UML使用可见性标记来为属性和操作的可见性建模。公有可见性通过在操作或属性前放置加号（+）表示；减号（−）表示私有可见性。图26.1显示了更新后的类图，其中包含可见性标记。[注：图26.1中不包含任何操作参数。这完全正常。添加可见性标记不会影响图25.18–25.21的类图中已经建模的参数。]

### 可导航性

在开始用C++实现我们的设计之前，我们介绍一个额外的UML表示法。图26.2中的类图通过向关联线添加可导航性箭头，进一步细化ATM系统中各类之间的关系。可导航性箭头（在类图中表示为带棒状箭头的箭头）指示关联可以沿哪个方向遍历，并基于通信图和顺序图中建模的协作（见25.8节）。在用UML设计系统并进行实现时，你使用可导航性箭头来帮助确定哪些对象需要引用或指向其他对象的指针。例如，从类ATM指向类BankDatabase的可导航性箭头表示我们可以从前一个导航到后一个，从而使ATM能够调用BankDatabase的操作。然而，由于图26.2不包含从类BankDatabase指向类ATM的可导航性箭头，BankDatabase不能访问ATM的操作。类图中两端都有可导航性箭头或完全没有可导航性箭头的关联表示**双向可导航性**——可以沿关联向任一方向导航。

与图25.10的类图一样，图26.2的类图省略了BalanceInquiry类和Deposit类，以保持图示简单。这些类所参与的关联的可导航性，与Withdrawal类关联的可导航性密切对应。回顾25.4节，BalanceInquiry与Screen类有一个关联。我们可以沿这个关联从BalanceInquiry类导航到Screen类，但不能从Screen类导航到BalanceInquiry类。因此，如果我们要在图26.2中为BalanceInquiry类建模，就会在这个关联的Screen类端放置一个可导航性箭头。还要回顾，Deposit类与Screen、Keypad和DepositSlot类关联。我们可以从Deposit类导航到这些类中的每一个，反之则不行。因此，我们在这些关联的Screen、Keypad和DepositSlot端放置可导航性箭头。[*注：* 在26.3节中，在我们通过融入面向对象概念中的继承来简化系统结构之后，会在最终类图中为这些额外的类和关联建模。]

## 根据 UML 设计实现 ATM 系统

现在准备开始实现ATM系统。我们首先将图26.1和图26.2中的类转换为C++头文件。这段代码将表示系统的“骨架”。在26.3节中，我们修改头文件以融入面向对象概念中的继承。在26.4节中，我们给出模型完整可工作的C++代码。

作为一个例子，我们从图26.1中Withdrawal类的设计开始开发该类头文件。我们使用这个图来确定类的属性和操作。我们使用图26.2中的UML模型来确定类之间的关联。我们对每个类遵循以下五条准则：

- 1. 使用类图中类第一个分隔栏中的名称在头文件中定义类（图26.3）。使用`#ifndef`、`#define`和`#endif`预处理指令防止头文件在程序中被多次包含。

```cpp
// Fig. 26.3: Withdrawal.h
// Definition of class Withdrawal that represents a withdrawal transaction
#ifndef WITHDRAWAL_H
#define WITHDRAWAL_H

class Withdrawal
{
}; // end class Withdrawal

#endif // WITHDRAWAL_H
```

**图 26.3** | 用预处理包装器包围的 Withdrawal 类定义。

- 2. 使用类第二个分隔栏中的属性声明数据成员。例如，Withdrawal类的私有属性`accountNumber`和`amount`生成图26.4中的代码。

```cpp
// Fig. 26.4: Withdrawal.h
// Definition of class Withdrawal that represents a withdrawal transaction
#ifndef WITHDRAWAL_H
#define WITHDRAWAL_H

class Withdrawal
{
private:
    // attributes
    int accountNumber; // account to withdraw funds from
    double amount; // amount to withdraw
}; // end class Withdrawal

#endif // WITHDRAWAL_H
```

**图 26.4** | 向 Withdrawal 类头文件添加属性。

- 3. 使用类图中描述的关联声明对其他对象的引用（或在适当处声明指针）。例如，根据图26.2，Withdrawal可以访问Screen类的一个对象、Keypad类的一个对象、CashDispenser类的一个对象和BankDatabase类的一个对象。Withdrawal类必须持有这些对象的句柄以向它们发送消息，因此图26.5的第19–22行声明四个引用作为私有数据成员。在26.4节Withdrawal类的实现中，构造函数用实际对象的引用初始化这些数据成员。第6–9行`#include`包含Screen、Keypad、CashDispenser和BankDatabase类定义的头文件，以便我们能在第19–22行声明对这些类对象的引用。

- 4. 事实证明，在图26.5中包含Screen、Keypad、CashDispenser和BankDatabase类的头文件超出了必要。Withdrawal类包含对这些类对象的引用——它不包含实际对象——而编译器创建引用所需的信息量与创建对象所需的信息量不同。回顾一下，创建对象要求你向编译器提供类的定义，而该定义
