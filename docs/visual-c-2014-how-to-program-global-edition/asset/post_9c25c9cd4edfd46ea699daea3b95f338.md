
# Self-Review Exercises 505

inheritance
heritance hierarchy
inherited member
inherited method
invoke a base-class constructor
invoke a base-class method
is relationship

override (redefine) a base-class method
private base-class member
protected base-class member
protected access modifier
public base-class member
Reference method of class object
single inheritance
allow copy
software reuse
standardized reusable components
ToString method of class object
virtual keyword

Memberwise method of class object
object class
object of the derived class
object of a base class
override keyword

# Self-Review Exercises

- 11.1 Fill in the blanks of the following statements:
a) ________ is a form of software reuse in which new classes acquire the members of existing classes and enhance those classes with new capabilities.
b) A base class's ________ members are accessed only in the base-class declaration and in derived-class declarations.
c) In a(n) ________ relationship, an object of a derived class can also be treated as an object of its base class.
d) In a(n) ________ relationship, a class object has references to objects of other classes as members.
e) In inheritance, a base class exists in a(n) ________ relationship with its derived classes.
f) A base class's ________ members are accessible anywhere the app has a reference to an object of that base class or to any of its derived classes.
g) When an object of a derived class is instantiated, a base class ________ called implicitly or explicitly.
h) Derived-class constructors can call base class constructors via the ________ keyword.

- 11.2 State whether each of the following is true or false. If false, explain why.
a) Base class constructors are not inherited by derived classes.
b) A has-a relationship is implemented via inheritance.
c) A Car has a is-relationship with the SteeringWheel and B classes.
d) Inheritance encourages the reuse of high-quality software.
e) When a derived class redefines a base-class method by using the same signature and runtime, the derived class is said to overload that base-class method.

# Answers to Self-Review Exercises

- 11.1 a) Inheritance. b) protected. c) is-a or inheritance. d) has-a or composition. e) hierarchical. f) public. g) constructor, h) base.

- 11.2 a) True. False. b) A has-a relationship is implemented via composition. c) Inheritance is implemented via inheritance. False. These are of has-a relationships. d) True. False. True. This is known as overriding, not overloading.

# Exercises

- 11.3 (Composition vs. Inheritance) Many apps with inheritance can be written with composition, and vice versa. Rewrite class BasePlusCommissionEmployee (Fig. 11.11) of the CommissionEmployee-BasePlusEmployee hierarchy to use composition rather than inheritance.

- 11.4 (Inheritance and Software Reuse) Discuss the ways in which inheritance promotes software reuse, saves time during development and prevents errors.

- 11.5 (Computer Device Inheritance) Draw a UML diagram for an inheritance hierarchy for computer devices a whereas the hierarchy shown in Fig. 12. Use ComputerDevice as the base of the hierarchy, then extend it with InputDevice, ProcessingDevice and OutputDevice. Continue to extend the hierarchy as deeply (i.e., as many levels) as possible. For example, Pointer, Keyboard and Scanner can extend the class InputDevice, CentralProcessing might extend ProcessingDevice, and Printer and Speaker might be classes of OutputDevice. [Note: You do not need to write any code for this exercise].

- 11.6 (Vehicle Inheritance) Draw a UML diagram for an inheritance hierarchy for Vehicle to mimic the hierarchy shown in Fig. 11.3. Draw all the vehicles you can think of—both MotorVehicle and NonVehicle—and form them into a complete vehicle hierarchy with many levels as possible. Your hierarchy should have class Vehicle at the top. Car MotorVehicle and NonVehicle should extend Vehicle. Add additional classes, such as Fuel, Electricity, WindPower, PoweredVehicle, etc., at their correct locations in the hierarchy as necessary.

- 11.7 (Chain of Constructor Classes) When the object of a derived class is instantiated, the chain of constructor calls that begin in the program. Discuss which constructor will be executed at the end. Can constructors be inherited?

- 11.8 (Quadrilateral Inheritance) Write an inheritance hierarchy for classes Quadrilateral, Parallelogram, Rectangle and Square. Quadrilateral as the base of the hierarchy. Make the hierarchy as deep (i.e., as many levels) as possible. Specify the instance variables, properties and methods for each class. The instance variables of Quadrilateral should be the x-y coordinate pairs for the four corners and outputs each Quadrilateral object area (except Quadrilateral).

- 11.9 (Account Inheritance Hierarchy) Create an inheritance hierarchy that a bank might use to represent ‘customers’ accounts. All customers in the bank can deposit (i.e., credit) money into their accounts and withdraw (i.e., debit) money from their accounts. More specific types of accounts also exist. Savings accounts, for earn interest on the money they hold. Checking accounts, on the other hand, charge a fee per transaction.

Create base Account and derived classes SavingsAccount and CheckingAccount that inherit from Account. Base Account should include one instance variable of type decimal to represent the balance. The class should provide a constructor that receives an initial balance and uses it to initialize the variable with a public property. The class should validate the initial balance to ensure it’s greater than or equal to 0.0; if not, throw an exception. The class should provide two public methods. Method Credit should add an amount to the current balance. Method Debit should withdraw money from the Account and ensure that the debit amount does not exceed the Account’s balance. If so, the balance should be unchanged, and the method should display the message “Debit exceeded balance.” The class should also provide a accessor in Balance that returns the current balance.

Derived SavingsAccount should inherit the functionality of an Account, but also include a decimal variable indicating the interest rate (percentage) to the Account. SavingsAccount constructor should receive the initial balance, as well as an initial value for the interest rate. SavingsAccount should provide public method CalculateInterest that returns a decimal indicating the amount of interest earned by an account. Method CalculateInterest should determine this amount by multiplying the interest rate by the account balance. [Note: SavingsAccount should inherit methods Credit and Debit without redefining them.]

![](img/57baed2319be0bb1b5f98674846f2711_506_0.png)

Derived CheckingAccount should inherit from base Account and include a decimal instance variable that represents the fee charged per transaction. CheckingAccount's constructor should receive the initial balance, as well as a parameter indicating a fee amount. CheckingAccount should redefine methods Credit and Debit so that they subtract the fee from the account balance whenever either transaction is performed successfully. CheckingAccount's versions of these methods should invoke the baseclass Account version to perform the updates to an account balance. CheckingAccount's Debit method should charge a fee only if money is actually withdrawn (i.e., the debit amount does not exceed the account balance). [Hint: Define Account's Debit method so that it returns a bool indicating whether money was withdrawn. Then use the return value to determine whether a fee should be charged.]

After defining the classes in this hierarchy, write an app that creates objects of each class and tests their methods. In the SavingsAccount object by first invoking its CalculateInterest method, then passing the returned interest amount to the object's Credit method.
