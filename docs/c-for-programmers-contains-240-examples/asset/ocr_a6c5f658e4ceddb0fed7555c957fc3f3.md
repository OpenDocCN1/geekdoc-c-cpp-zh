tant for the destructors of both the derived class and base class to execute. The base-class destructor automatically executes after the derived-class destructor.

# Error-Prevention Tip 13.2

> If a class has virtual functions, provide a virtual destructor, even if one is not required for the class. This ensures that a custom derived-class destructor (if there is one) will be invoked when a derived-class object is deleted via a base class pointer.

# Common Programming Error 13.5

> Constructors cannot be virtual. Declaring a constructor virtual is a compilation error.

# 13.10 (Optional) Software Engineering Case Study: Incorporating Inheritance into the ATM System

We now revisit our ATM system design to see how it might benefit from inheritance. To apply inheritance, we first look for commonality among classes in the system. We create an inheritance hierarchy to model similar (yet not identical) classes in a more efficient and elegant manner that enables us to process objects of these classes polymorphically. We then modify our class diagram to incorporate the new inheritance relationships. Finally, we demonstrate how our updated design is translated into C++ header files.

In Section 3.11, we encountered the problem of representing a financial transaction in the system. Rather than create one class to represent all transaction types, we decided to create three individual transaction classes—BalanceInquiry, Withdrawal and Deposit—to represent the transactions that the ATM system can perform. Figure 13.26 shows the attributes and operations of these classes. Note that they have one attribute (accountNumber) and one operation (execute) in common. Each class requires attribute accountNumber to specify the account to which the transaction applies. Each class contains operation execute, which the ATM invokes to perform the transaction. Clearly, BalanceInquiry, Withdrawal and Deposit represent types of transactions. Figure 13.26 reveals commonality among the transaction classes, so using inheritance to factor out the common features seems appropriate for designing these classes. We place the common functionality in base class Transaction and derive classes BalanceInquiry, Withdrawal and Deposit from Transaction (Fig. 13.27).

![](bbox=[0.17, 0.75, 0.83, 0.92])

Fig. 13.26 | Attributes and operations of classes BalanceInquiry, Withdrawal and Deposit.