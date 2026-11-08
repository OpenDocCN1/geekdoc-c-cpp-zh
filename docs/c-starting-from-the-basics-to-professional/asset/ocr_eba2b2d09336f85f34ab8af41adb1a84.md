Each LoanAccount object contains all the members that a BankAccount object does, but it has the option of defining new members of its own or of redefining the functions it inherits so that they are more meaningful in its context. Redefining a base class's function in a derived class is called overriding; the latter function is said to override the former. This last ability is very powerful, as you'll see.

Extending the current example, you might also want to create a new CheckingAccount type by adding different characteristics to BankAccount. This situation is illustrated in Figure 12-4.

![](bbox=[0.15, 0.265, 0.83, 0.525])

*Figure 12-4. An example of inheritance*

Both of the LoanAccount and CheckingAccount types are defined so that they are derived from the type BankAccount. They inherit the member variables and member functions of BankAccount, but they are free to define new characteristics that are specific to their own type.

In this example, CheckingAccount has added a member variable called overdraftFacility that is unique to itself, and both the derived classes can override any of the member functions that they inherit from the base class. It's likely they would override calcInterest(), for example, because calculating and dealing with the interest for a checking account involves something rather different than doing it for a loan account.

# ## Polymorphism

*Polymorphism* means the ability to assume different forms at different times. Polymorphism in C++ always involves calling a member function of an object using either a pointer or a reference. Such function calls can have different effects at different times—sort of *Jekyll and Hyde* function calls. The mechanism works only

¹ Technically speaking, programming language theory distinguishes several different forms of polymorphism. What we refer to here as “polymorphism” is formally known as subtyping, subtype polymorphism, or inclusion polymorphism. Other forms of polymorphism that are also supported by C++ include parametric polymorphism (C++ function and class templates; see Chapters 10 and 17) and ad hoc polymorphism (function and operator overloading; see Chapters 8 and 13). In the world of object-oriented programming, however, the term “polymorphism” usually refers solely to subtyping, so that is also the terminology we adopt in this book.