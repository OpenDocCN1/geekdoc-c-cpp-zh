
## Identifying and Modeling Operation Parameters for Class CashDispenser

Figure 12.21 specifies that operation dispenseCash of class CashDispenser takes a Double parameter amount to indicate the amount of cash (in dollars) to be dispensed. Operation isSufficientCashAvailable also takes a Double parameter amount to indicate the amount of cash in question.

```
CashDispenser
count : Integer = 500
dispenseCash( amount : Double )
isSufficientCashAvailable( amount : Double ) : Boolean
```

Fig. 12.21 | Class CashDispenser with operation parameters.

## Identifying and Modeling Operation Parameters for Other Classes

We do not discuss parameters for operation execute of classes BalanceInquiry, Withdrawal and Deposit, operation getInput of class Keypad and operation isEnvelopeReceived of class DepositSlot. At this point in our design process, we cannot determine whether these operations require additional data, so we leave their parameter lists empty. Later, we may decide to add parameters.

In this section, we’ve determined many of the operations performed by the classes in the ATM system. We’ve identified the parameters and return types of some of the operations. As we continue our design process, the number of operations belonging to each class may vary—we might find that new operations are needed or that some current operations are unnecessary. We also might determine that some of our class operations need additional parameters and different return types, or that some parameters are unnecessary or require different types.

## Self-Review Exercises for Section 12.6

- 12.14 Which of the following is not a behavior?
  - a) reading data from a file
  - b) printing output
  - c) text output
  - d) obtaining input from the user

- 12.15 If you were to add to the ATM system an operation that returns the amount attribute of class Withdrawal, how and where would you specify this operation in the class diagram of Fig. 12.17?

- 12.16 Describe the meaning of the following operation listing that might appear in a class diagram for an object-oriented design of a calculator:

  `add( x : Integer, y : Integer ) : Integer`

## 12.7 Indicating Collaboration Among Objects

[Note: This section can be taught after Chapter 7.]

In this section, we concentrate on the collaborations (interactions) among objects. When two objects communicate with each other to accomplish a task, they’re said to collaborate—objects do this by invoking one another’s operations. A collaboration consists of an object of one class sending a message to an object of another class. Messages are sent in Java via method calls.

In Section 12.6, we determined many of the operations of the system’s classes. Now, we concentrate on the messages that invoke these operations. To identify the collaborations in the system, we return to the requirements document in Section 12.2. Recall that this document specifies the range of activities that occur during an ATM session (e.g., authenticating a user, performing transactions). The steps used to describe how the system must perform each of these tasks are our first indication of the collaborations in our system. As we proceed through this section and Chapter 13, we may discover additional collaborations.

### Identifying the Collaborations in a System

We identify the collaborations in the system by carefully reading the sections of the requirements document that specify what the ATM should do to authenticate a user and to perform each transaction type. For each action or step described, we decide which objects in our system must interact to achieve the desired result. We identify one object as the sending object and another as the receiving object. We then select one of the receiving object’s operations (identified in Section 12.6) that must be invoked by the sending object to produce the proper behavior. For example, the ATM displays a welcome message when idle. We know that an object of class Screen displays a message to the user via its displayMessage operation. Thus, we decide that the system can display a welcome message by employing a collaboration between the ATM and the Screen in which the ATM sends a displayMessage message to the Screen by invoking the displayMessage operation of class Screen. [Note: To avoid repeating the phrase “an object of class...,” we refer to an object by using its class name preceded by an article (e.g., “a,” “an” or “the”)—for example, “the ATM” refers to an object of class ATM.]

Figure 12.22 lists the collaborations that can be derived from the requirements document. For each sending object, we list the collaborations in the order in which they first occur during an ATM session (i.e., the order in which they’re discussed in the requirements document). We list each collaboration involving a unique sender, message and recipient only once, even though the collaborations may occur at several different times throughout an ATM session. For example, the first row in Fig. 12.22 indicates that the ATM collaborates with the Screen whenever the ATM needs to display a message to the user.

Let’s consider the collaborations in Fig. 12.22. Before allowing a user to perform any transactions, the ATM must prompt the user to enter an account number, then to enter a PIN. It accomplishes these tasks by sending a displayMessage message to the Screen. Both actions refer to the same collaboration between the ATM and the Screen, which is already listed in Fig. 12.22. The ATM obtains input in response to a prompt by sending a getInput message to the Keypad. Next, the ATM must determine whether the user-specified account number and PIN match those of an account in the database. It does so by sending an authenticateUser message to the BankDatabase. Recall that the BankDatabase cannot authenticate a user directly—only the user’s Account (i.e., the Account that contains the account number specified by the user) can access the user’s PIN on record to authenticate the user. Figure 12.22 therefore lists a collaboration in which the BankDatabase sends a validatePIN message to an Account.

After the user is authenticated, the ATM displays the main menu by sending a series of displayMessage messages to the Screen and obtains input containing a menu selection by sending a getInput message to the Keypad. We’ve already accounted for these collaborations, so we do not add anything to Fig. 12.22. After the user chooses a type of transaction to perform, the ATM executes the transaction by sending an execute message to an object of the appropriate transaction class (i.e., a BalanceInquiry, a Withdrawal or a Deposit). For example, if the user chooses to perform a balance inquiry, the ATM sends an execute message to a BalanceInquiry.

| An object of class... | sends the message... | to an object of class... |
| --- | --- | --- |
| ATM | displayMessage | Screen |
| ATM | getInput | Keypad |
| ATM | authenticateUser | BankDatabase |
| ATM | execute | BalanceInquiry |
| ATM | execute | Withdrawal |
| ATM | execute | Deposit |
| BalanceInquiry | getAvailableBalance | BankDatabase |
| BalanceInquiry | getTotalBalance | BankDatabase |
| BalanceInquiry | displayMessage | Screen |
| Withdrawal | displayMessage | Screen |
| Withdrawal | getInput | Keypad |
| Withdrawal | getAvailableBalance | BankDatabase |
| Withdrawal | isSufficientCashAvailable | CashDispenser |
| Withdrawal | debit | BankDatabase |
| Withdrawal | dispenseCash | CashDispenser |
| Deposit | displayMessage | Screen |
| Deposit | getInput | Keypad |
| Deposit | isEnvelopeReceived | DepositSlot |
| Deposit | credit | BankDatabase |
| BankDatabase | validatePIN | Account |
| BankDatabase | getAvailableBalance | Account |
| BankDatabase | getTotalBalance | Account |
| BankDatabase | debit | Account |
| BankDatabase | credit | Account |

Fig. 12.22 | Collaborations in the ATM system.

Further examination of the requirements document reveals the collaborations involved in executing each transaction type. A BalanceInquiry retrieves the amount of money available in the user’s account by sending a getAvailableBalance message to the BankDatabase, which responds by sending a getAvailableBalance message to the user’s Account. Similarly, the BalanceInquiry retrieves the amount of money on deposit by sending a getTotalBalance message to the BankDatabase, which sends the same message to the user’s Account. To display both parts of the user’s account balance at the same time, the BalanceInquiry sends a displayMessage message to the Screen.

A Withdrawal responds to an execute message by sending displayMessage messages to the Screen to display a menu of standard withdrawal amounts (i.e., $20, $40, $60, $100, $200). The Withdrawal sends a getInput message to the Keypad to obtain the user’s selection. Next, the Withdrawal determines whether the requested amount is less than or equal
