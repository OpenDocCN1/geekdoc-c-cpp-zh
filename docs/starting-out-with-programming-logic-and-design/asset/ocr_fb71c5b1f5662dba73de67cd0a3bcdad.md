# 564 Chapter 14 Object-Oriented Programming

+   6. Polymorphism allows a class variable of the superclass type to reference objects of either the superclass or the subclass types.

# Short Answer

+   1. What is encapsulation?
2. Why is an object's internal data usually hidden from outside code?
3. What is the difference between a class and an instance of a class?
4. In many programming languages, what does the new key word do?
5. The following pseudocode statement calls an object's method. What is the name of the method? What is the name of the variable that references the object?
Call wallet.get()
6. What is stale data?
7. What does a subclass inherit from its superclass?
8. Looking at the following pseudocode, which is the first line of a class definition. What is the name of the superclass? What is the name of the subclass?
Class Tiger Extends Felis

# Algorithm Workbench

+   1. Suppose myCar is the name of a class variable that references an object, and go is the name of a method. (The go method does not take any arguments.) Write a pseudocode statement that uses the myCar variable to call the method.
2. Look at this partial definition, and then follow the subsequent instructions:
Class Book
Private String title
Private String author
Private String publisher
Private Integer copiesSold
End Class
a. Write a constructor for this class. The constructor should accept an argument for each of the fields.
b. Write accessor and mutator methods for each field.
c. Draw a UML diagram for the class, including the methods you have written.
3. Look at the following description of a problem domainnThe bank offers the following types of accounts to its customers: savings accounts, checking accounts, and money market accounts. Customers are allowed to deposit money into an account (increasing its balance), withdraw money from an account (thereby decreasing its balance), and earn interest on the account. Each account has an interest rate.
Assume that you are writing a program that will calculate the amount of interest earned for a bank.
a. Identify the potential classes in this problem domain.
b. Refine the list to include only the necessary class or classes for this problem.
c. Identify the responsibilities of the class or classes.