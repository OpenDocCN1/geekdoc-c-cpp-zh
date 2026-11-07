
the program’s general portions. We used a detailed illustration to help you understand how runtime polymorphism, virtual functions and dynamic binding can be implemented “under the hood.”

We initially focused on implementation inheritance, then pointed out that decades of experience with real-world, business-critical and mission-critical systems have shown that it can be difficult to maintain and modify such systems. So, we refactored our `Employee` payroll example to use interface inheritance in which the base class contained only pure `virtual` functions that derived concrete classes were required to implement. In that example, we introduced the composition-and-dependency-injection approach in which a class contains a pointer to an object that provides behaviors required by objects of the class. Then, we discussed how this interface-based approach makes the example easier to modify and evolve.

A key goal of this chapter was to familiarize you with inheritance mechanics and runtime polymorphism with `virtual` functions. Now, you’ll be able to better appreciate newer polymorphism idioms and techniques we show later in the book that can promote ease of modifiability and better performance.

In Chapter 11, we continue our object-oriented programming presentation with operator overloading, which enables existing operators to work with custom class objects. For example, you’ll see how to overload the `<<` operator to output a complete array without explicitly using an iteration statement. You’ll use “smart pointers” to manage dynamically allocated memory and ensure that it’s released when no longer needed. We’ll introduce the remaining special member functions and discuss rules and guidelines for using them. We’ll consider move semantics, which enable object resources (such as dynamically allocated memory) to move from one object to another when an object is going out of scope. As you’ll see, this can save memory and increase performance.

## Exercises

- 10.1 **(Inheritance Advantage)** Discuss how inheritance saves time during program development and helps prevent errors.
- 10.2 **(Programming in the General)** How is it that polymorphism enables you to program “in the general” rather than “in the specific”? Discuss the advantages of programming “in the general.”
- 10.3 **(Inheriting Interface vs. Implementation)** Distinguish between inheriting interface and inheriting implementation. How do inheritance hierarchies designed for inheriting interface differ from those designed for inheriting implementation?
- 10.4 **(Virtual Functions)** What are `virtual` functions? Describe a circumstance in which `virtual` functions would be appropriate.
- 10.5 **(Dynamic Binding vs. Static Binding)** Distinguish between static binding and dynamic binding. Explain the use of `virtual` functions and the `vtable` in dynamic binding.
- 10.6 **(Virtual Functions vs. Pure Virtual Functions)** Distinguish between `virtual` functions and pure `virtual` functions.
- 10.7 **(Polymorphism and Extensibility)** How does polymorphism promote extensibility?

### Inheritance Exercises

- **10.8** *(Student Inheritance Hierarchy)* Draw an inheritance hierarchy for university students like the one in Section 10.2.1. Use Student as the base class of the hierarchy, then include classes UndergraduateStudent and GraduateStudent that derive from Student. Continue to extend the hierarchy to many levels. For example, Freshman, Sophomore, Junior and Senior might derive from UndergraduateStudent, and DoctoralStudent and MastersStudent might derive from GraduateStudent. [*Note:* You do not need to write any code for this exercise.]
- **10.9** *(Quadrilateral Inheritance Hierarchy)* Draw an inheritance hierarchy for classes Quadrilateral, Trapezoid, Parallelogram, Rectangle and Square. Use Quadrilateral as the base class of the hierarchy.
- **10.10** *(Richer Shape Hierarchy)* The world of shapes is much richer than the shapes included in the inheritance hierarchy of Section 10.2.2. Write down all the shapes you can think of—both two-dimensional and three-dimensional—and form them into a more complete Shape hierarchy with as many levels as possible. Your hierarchy should have the base-class Shape from which class TwoDimensionalShape and class ThreeDimensionalShape are derived. [*Note:* You do not need to write any code for this exercise.]
- **10.11** *(Composition as an Alternative to Inheritance)* Many inheritance hierarchies can be written with composition instead. Rewrite class SalariedCommissionEmployee from Section 10.3.2. Rather than inheriting from class SalariedEmployee, use composition. So, a SalariedCommissionEmployee should have a SalariedEmployee object as a data member. Ensure that class SalariedCommissionEmployee’s interface includes the member functions previously inherited from class SalariedEmployee—each should call the corresponding member function on the composed SalariedEmployee object. After you do this, assess the relative merits of the two approaches for designing classes SalariedEmployee and SalariedCommissionEmployee. Which approach is more natural? Why?
- **10.12** *(Account Inheritance Hierarchy)* Create an inheritance hierarchy that a bank might use to represent customers’ bank accounts. All customers at this bank can deposit money into their accounts and withdraw money from their accounts. More specific types of accounts also exist. Savings accounts, for instance, earn interest on the money they hold, whereas checking accounts charge a fee per transaction.

  Create an inheritance hierarchy containing base-class Account. The derived classes SavingsAccount and CheckingAccount inherit from Account. Class Account should include one data member of type cpp_dec_float_50 (from Boost Multiprecision; Section 4.14) to represent the account balance. The class should provide:

  - A constructor—The constructor should receive an initial balance and use it to initialize the data member. Validate the initial balance to ensure it’s greater than or equal to 0.0. If not, the balance should be set to 0.0, and the constructor should display an error message indicating that the initial balance was invalid.
  - Member function `deposit`—This function deposits money into the Account, ensuring the deposit amount is positive and, if not, throws an `invalid_argument` exception.
  - Member function `withdraw`—This function withdraws money from the Account, ensuring the withdrawal amount is positive and does not exceed the Account’s balance. If the withdrawal amount is invalid, throw an `invalid_argument` exception with an appropriate message.
  - Member function `getBalance`—This function returns the current balance.

  Derived-class `SavingsAccount` should inherit the functionality of an Account and include a data member of type `cpp_dec_float_50` (from Boost Multiprecision) indicating the interest rate (percentage) assigned to the Account. The class should provide:

  - A constructor—The constructor should receive the initial balance and an initial value for the interest rate.
  - Member function `calculateInterest`—This function returns an object of type `cpp_dec_float_50` representing the amount of interest earned by an account. The interest amount is the interest rate (such as 0.05 for 5%) times the account balance.

  `SavingsAccount` should inherit member functions `deposit` and `withdraw` as is without redefining them.

  Derived-class `CheckingAccount` should inherit from base-class Account and include an additional data member of type `cpp_dec_float_50` (from Boost Multiprecision) that represents the fee charged per transaction. The class should provide:

  - A constructor—The constructor receives the initial balance and the fee amount per transaction.
  - Redefined member functions `deposit` and `withdraw`—These functions subtract the fee from the account balance whenever either transaction is performed successfully. Functions `deposit` and `withdraw` should invoke their base-class Account versions to update the account balance. The `withdraw` function should charge a fee only if money is actually withdrawn (i.e., the amount does not exceed the account balance).

  *Hint:* Define Account’s `withdraw` function to return a bool indicating whether money was withdrawn. Then use the return value to determine whether a fee should be charged.

  After defining the Account hierarchy, write a program that creates one object of each class and tests its member functions.

### Polymorphism Exercises

- **10.13** *(Payroll-System Modification)* Modify the payroll system of Section 10.9 to include private data member `m_birthDate` in class Employee. Use class Date from Figs. 9.25–9.26 to represent an employee’s birthday. Assume that payroll is processed once per month. Create a vector of Employee pointers to store the various employee objects. In a loop, calculate the payroll for each Employee polymorphically, and add a $100.00 bonus to the person’s payroll amount if the current month is the month in which the Employee’s birthday occurs.
- **10.14** *(Polymorphic Banking Program Using Account Hierarchy)* Develop a polymorphic banking program using the Account hierarchy created in Exercise 10.12. Modify the `deposit` and `withdraw` functions in class Account to be virtual functions to enable poly-
