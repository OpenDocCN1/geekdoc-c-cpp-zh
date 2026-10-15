
## Performance Tip 6.9

Avoid using recursion in performance situations. Recursive calls take time and consume additional memory.

## Common Programming Error 6.26

Accidentally having a nonrecursive function call itself, either directly or indirectly (through another function), is a logic error.

## 6.22 (Optional) Software Engineering Case Study: Identifying Class Operations in the ATM System

In the Software Engineering Case Study sections at the ends of Chapters 3, 4 and 5, we performed the first few steps in the object-oriented design of our ATM system. In Chapter 3, we identified the classes that we’ll need to implement and we created our first class diagram. In Chapter 4, we described some attributes of our classes. In Chapter 5, we examined object states and modeled object state transitions and activities. Now, we determine some of the class operations (or behaviors) needed to implement the ATM system.

### Identifying Operations

An operation is a service that objects of a class provide to clients of the class. Consider the operations of some real-world objects. A radio’s operations include setting its station and volume (typically invoked by a person adjusting the radio’s controls). A car’s operations include accelerating (invoked by the driver pressing the accelerator pedal), decelerating (invoked by the driver pressing the brake pedal or releasing the gas pedal), turning and shifting gears. Software objects can offer operations as well—for example, a software graphics object might offer operations for drawing a circle, drawing a line, drawing a square and the like. A spreadsheet software object might offer operations like printing the spreadsheet, totaling the elements in a row or column and graphing information in the spreadsheet as a bar chart or pie chart.

We can derive many of the operations of each class by examining the key verbs and verb phrases in the requirements specification. We then relate each of these to particular classes in our system (Fig. 6.32). The verb phrases in Fig. 6.32 help us determine the operations of each class.

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

To create the updated class diagram of Fig. 6.33, we first identify operations by examining the verb phrases listed for each class in Fig. 6.32. The “executes financial transactions” phrase associated with class ATM implies that class ATM instructs transactions to execute.

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_265_0.png)

Fig. 6.33 | Classes in the ATM system with attributes and operations.

Therefore, classes BalanceInquiry, Withdrawal and Deposit each need an operation to provide this service to the ATM. We place this operation (which we have named execute) in the third compartment of the three transaction classes in the class diagram of Fig. 6.33. During an ATM session, the ATM object will invoke the execute operation of each transaction object to tell it to execute.

The UML represents operations (which are implemented as member functions in C++) by listing the operation name, followed by a comma-separated list of parameters in parentheses, a colon and the return type:

```
operationName( parameter1, parameter2, ..., parameterN ) : return type
```

Each parameter in the comma-separated parameter list consists of a parameter name, followed by a colon and the parameter type:

```
parameterName : parameterType
```

For the moment, we do not list the parameters of our operations—we’ll identify and model the parameters of some of the operations shortly. For some, we do not yet know the return types, so we also omit them from the diagram. These omissions are perfectly normal at this point. As our design and implementation proceed, we’ll add the remaining return types.

### Operations of Class BankDatabase and Class Account

Figure 6.32 lists the phrase “authenticates a user” next to class BankDatabase—the database is the object that contains the account information necessary to determine whether the account number and PIN entered by a user match those of an account held at the bank. Therefore, class BankDatabase needs an operation that provides an authentication service to the ATM. We place the operation authenticateUser in the third compartment of class BankDatabase (Fig. 6.33). However, an object of class Account, not class BankDatabase, stores the account number and PIN that must be accessed to authenticate a user, so class Account must provide a service to validate a PIN obtained through user input against a PIN stored in an Account object. Therefore, we add a validatePIN operation to class Account. Note that we specify a return type of Boolean for the authenticateUser and validatePIN operations. Each operation returns a value indicating either that the operation was successful in performing its task (i.e., a return value of true) or that it was not (i.e., a return value of false).

Figure 6.32 lists several additional verb phrases for class BankDatabase: “retrieves an account balance,” “credits a deposit amount to an account” and “debits a withdrawal amount from an account.” Like “authenticates a user,” these remaining phrases refer to services that the database must provide to the ATM, because the database holds all the account data used to authenticate a user and perform ATM transactions. However, objects of class Account actually perform the operations to which these phrases refer. Thus, we assign an operation to both class BankDatabase and class Account to correspond to each of these phrases. Recall from Section 3.11 that, because a bank account contains sensitive information, we do not allow the ATM to access accounts directly. The database acts as an intermediary between the ATM and the account data, thus preventing unauthorized access. As we’ll see in Section 7.12, class ATM invokes the operations of class BankDatabase, each of which in turn invokes the operation with the same name in class Account.

The phrase “retrieves an account balance” suggests that classes BankDatabase and Account each need a getBalance operation. However, recall that we created two attributes in class Account to represent a balance—availableBalance and totalBalance. A balance inquiry requires access to both balance attributes so that it can display them to the user, but a withdrawal needs to check only the value of availableBalance. To allow objects in the system to obtain each balance attribute individually, we add operations getAvailableBalance and getTotalBalance to the third compartment of classes BankDatabase and Account (Fig. 6.33). We specify a return type of Double for each of these operations, because the balance attributes which they retrieve are of type Double.

The phrases “credits a deposit amount to an account” and “debits a withdrawal amount from an account” indicate that classes BankDatabase and Account must perform operations to update an account during a deposit and withdrawal, respectively. We therefore assign credit and debit operations to classes BankDatabase and Account. You may recall that crediting an account (as in a deposit) adds an amount only to the totalBalance attribute. Debiting an account (as in a withdrawal), on the other hand, subtracts the amount from both balance attributes. We hide these implementation details inside class Account. This is a good example of encapsulation and information hiding.

If this were a real ATM system, classes BankDatabase and Account would also provide a set of operations to allow another banking system to update a user’s account balance after either confirming or rejecting all or part of a deposit. Operation confirmDepositAmount, for example, would add an amount to the availableBalance attribute, thus making deposited funds available for withdrawal. Operation rejectDepositAmount would subtract an amount from the totalBalance attribute to indicate that a specified amount, which had recently been deposited through the ATM and added to the totalBalance, was not found in the deposit envelope. The bank would invoke this operation after determining either that the user failed to include the correct amount of cash or that any checks did not clear (i.e., they “bounced”). While adding these operations would make our system more complete, we do not include them in our class diagrams or our implementation because they are beyond the scope of the case study.

### Operations of Class Screen

Class Screen “displays a message to the user” at various times in an ATM session. All visual output occurs through the screen of the ATM. The requirements specification describes many types of messages (e.g., a welcome message, an error message, a thank you message) that the screen displays to the user. The requirements specification also indicates that the screen displays prompts and menus to the user. However, a prompt is really just a message describing what the user should input next, and a menu is essentially a type of prompt consisting of a series of messages (i.e., menu options) displayed consecutively. Therefore, rather than assign class Screen an individual operation to display each type of message, prompt and menu, we simply create one operation that can display any message specified by a parameter. We place this operation (displayMessage) in the third compartment of class Screen in our class diagram (Fig. 6.33). Note that we do not worry about the parameter of this operation at this time—we model the parameter later in this section.

### Operations of Class Keypad

From the phrase “receives numeric input from the user” listed by class Keypad in Fig. 6.32, we conclude that class Keypad should perform a getInput operation. Because the ATM's
