
![](img/bfd978e7e9b192bab46ec2a89e481263_1135_0.png)

**Fig. 25.21** | Class CashDispenser with operation parameters.

whether these operations require additional data to perform their tasks, so we leave their parameter lists empty. As we progress through the case study, we may decide to add parameters to these operations.

In this section, we’ve determined many of the operations performed by the classes in the ATM system. We’ve identified the parameters and return types of some of the operations. As we continue our design process, the number of operations belonging to each class may vary—we might find that new operations are needed or that some current operations are unnecessary—and we might determine that some of our class operations need additional parameters and different return types.

## Self-Review Exercises for Section 25.7

- **25.14** Which of the following is not a behavior?
  - a) reading data from a file
  - b) printing output
  - c) text output
  - d) obtaining input from the user

- **25.15** If you were to add to the ATM system an operation that returns the amount attribute of class `Withdrawal`, how and where would you specify this operation in the class diagram of Fig. 25.17?

- **25.16** Describe the meaning of the following operation listing that might appear in a class diagram for an object-oriented design of a calculator:

  ```
  add( x : Integer, y : Integer ) : Integer
  ```

## 25.8 Indicating Collaboration Among Objects

> **[Note:** This section can be studied after Chapter 7.]

In this section, we concentrate on the collaborations (interactions) among objects in our ATM system. When two objects communicate with each other to accomplish a task, they are said to **collaborate**—they do this by invoking one another’s operations. A **collaboration** consists of an object of one class sending a **message** to an object of another class. Messages are sent in C++ via member-function calls.

In Section 25.7, we determined many of the operations of the system’s classes. Next, we concentrate on the messages that invoke these operations. To identify the collaborations, we return to the requirements document in Section 25.3. Recall that this document specifies the range of activities that occur during an ATM session (e.g., authenticating a user, performing transactions). The steps used to describe how the system must perform each of these tasks are our first indication of the collaborations in our system. As we proceed through this and the remaining sections, we may discover additional collaborations.

| An object of class... | sends the message... | to an object of class... |
|---|---|---|
| BankDatabase | validatePIN | Account |
|  | getAvailableBalance | Account |
|  | getTotalBalance | Account |
|  | debit | Account |
|  | credit | Account |

**Fig. 25.22** Collaborations in the ATM system. (Part 2 of 2.)

Let’s consider the collaborations in Fig. 25.22. Before allowing a user to perform any transactions, the ATM must prompt the user to enter an account number, then to enter a PIN. It accomplishes each of these tasks by sending a `displayMessage` message to the Screen. Both of these actions refer to the same collaboration between the ATM and the Screen, which is already listed in Fig. 25.22. The ATM obtains input in response to a prompt by sending a `getInput` message to the Keypad. Next, the ATM must determine whether the user-specified account number and PIN match those of an account in the database. It does so by sending an `authenticateUser` message to the BankDatabase. Recall that the BankDatabase cannot authenticate a user directly—only the user’s Account (i.e., the Account that contains the account number specified by the user) can access the user’s PIN to authenticate the user. Figure 25.22 therefore lists a collaboration in which the BankDatabase sends a `validatePIN` message to an Account.

After the user is authenticated, the ATM displays the main menu by sending a series of `displayMessage` messages to the Screen and obtains input containing a menu selection by sending a `getInput` message to the Keypad. We’ve already accounted for these collaborations. After the user chooses a type of transaction to perform, the ATM executes the transaction by sending an `execute` message to an object of the appropriate transaction class (i.e., a `BalanceInquiry`, a `Withdrawal` or a `Deposit`). For example, if the user chooses to perform a balance inquiry, the ATM sends an `execute` message to a `BalanceInquiry`.

Further examination of the requirements document reveals the collaborations involved in executing each transaction type. A `BalanceInquiry` retrieves the amount of money available in the user’s account by sending a `getAvailableBalance` message to the BankDatabase, which responds by sending a `getAvailableBalance` message to the user’s Account. Similarly, the `BalanceInquiry` retrieves the amount of money on deposit by sending a `getTotalBalance` message to the BankDatabase, which sends the same message to the user’s Account. To display both measures of the user’s balance at the same time, the `BalanceInquiry` sends a `displayMessage` message to the Screen.

A Withdrawal sends the Screen several `displayMessage` messages to display a menu of standard withdrawal amounts (i.e., $20, $40, $60, $100, $200). The Withdrawal sends the Keypad a `getInput` message to obtain the user’s menu selection, then determines whether the requested withdrawal amount is less than or equal to the user’s account balance. The Withdrawal can obtain the amount of money available in the account by sending the BankDatabase a `getAvailableBalance` message. The Withdrawal then tests whether the cash dispenser contains enough cash by sending the CashDispenser an `isSufficientCashAvailable` message. A Withdrawal sends the BankDatabase a debit message to decrease the user’s account balance. The BankDatabase sends the same message to the appropriate Account. Recall that debiting funds from an Account decreases both the `totalBalance` and the `availableBalance`. To dispense the requested amount of cash, the `Withdrawal` sends the `CashDispenser` a `dispenseCash` message. Finally, the `Withdrawal` sends a `displayMessage` message to the `Screen`, instructing the user to take the cash.

A Deposit responds to an execute message first by sending a `displayMessage` message to the Screen to prompt the user for a deposit amount. The Deposit sends a `getInput` message to the Keypad to obtain the user’s input. The Deposit then sends a `displayMessage` message to the Screen to tell the user to insert a deposit envelope. To determine whether the deposit slot received an incoming deposit envelope, the Deposit sends an `isEnvelopeReceived` message to the DepositSlot. The Deposit updates the user’s account by sending a credit message to the BankDatabase, which subsequently sends a credit message to the user’s Account. Recall that crediting funds to an Account increases the `totalBalance` but not the `availableBalance`.

### Interaction Diagrams

Now that we’ve identified possible collaborations between the objects in our ATM system, let’s graphically model these interactions using the UML. Several types of [interaction diagrams](#) model the behavior of a system by showing how objects interact with one another. The [communication diagram](#) emphasizes which objects participate in collaborations. **[Note:** Communication diagrams were called [collaboration diagrams](#) in earlier versions of the UML.] Like the communication diagram, the [sequence diagram](#) shows collaborations among objects, but it emphasizes *when* messages are sent between objects *over time*.

### Communication Diagrams

Figure 25.23 shows a communication diagram that models the ATM executing a `BalanceInquiry`. Objects are modeled in the UML as rectangles containing names in the form `objectName : ClassName`. In this example, which involves only one object of each type, we display the object name and list only a colon followed by the class name. **[Note:** Specifying the name of each object in a communication diagram is recommended when modeling multiple objects of the same type.] Communication objects are connected with solid lines, and messages are passed between objects along these lines in the direction shown by arrows. The name of the message, which appears next to the arrow, is the name of an operation (i.e., a member function) belonging to the receiving object—think of the name as a verb describing the service the receiving object provides to sending objects (its “clients”).

![](img/bfd978e7e9b192bab46ec2a89e481263_1138_0.png)

**Fig. 25.23** Communication diagram of the ATM executing a balance inquiry.

The solid filled arrow in Fig. 25.23 represents a message—or *synchronous call*—in the UML and a function call in C++. This arrow indicates that the flow of control is from the sending object (the ATM) to the receiving object (a BalanceInquiry). Since this is a *synchronous call*, the sending object may not send another message, or do anything at all, until the receiving object processes the message and returns control to the sending object—the sender just
