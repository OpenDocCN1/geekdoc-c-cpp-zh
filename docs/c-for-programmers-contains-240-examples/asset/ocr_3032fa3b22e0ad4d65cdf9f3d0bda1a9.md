![](bbox=[0.167, 0.108, 0.837, 0.554])

图 4.20 | Classes with attributes.

not consider the user to be authenticated. If an attribute has no initial value specified, only its name and type (separated by a colon) are shown. For example, the accountNumber attribute of class BalanceInquiry is an Integer. Here we show no initial value, because the value of this attribute is a number that we do not yet know—it will be determined at execution time based on the account number entered by the current ATM user.

Figure 4.20 does not include any attributes for classes Screen, Keypad and DepositSlot. These are important components of our system, for which our design process simply has not yet revealed any attributes. We may still discover some, however, in the remaining design phases or when we implement these classes in C++. This is perfectly normal for the iterative process of software engineering.

> **Software Engineering Observation 4.3**
> 
> *At the early stages in the design process, classes often lack attributes (and operations). Such classes should not be eliminated, however, because attributes (and operations) may become evident in the later phases of design and implementation.*

Note that Fig. 4.20 also does not include attributes for class BankDatabase. Recall from Chapter 3 that in C++, attributes can be represented by either fundamental types or class types. We have chosen to include only fundamental-type attributes in the class diagram in Fig. 4.20 (and in similar class diagrams throughout the case study). A class-type