
For the class `calendarType`, include the following operations:

- a. Determine the first day of the month for which the calendar will be printed. Call this operation `firstDayOfMonth`.
- b. Set the month.
- c. Set the year.
- d. Return the month.
- e. Return the year.
- f. Print the calendar for the particular month.
- g. Add the appropriate constructors to initialize the member variables.

- 10. a. Write the definitions of the member functions of the class `calendarType` (designed in Programming Exercise 9) to implement the operations of the class `calendarType`.
- b. Write a test program to print the calendar for either a particular month or a particular year. For example, the calendar for September 2015 is:

**September 2015**

| Sun | Mon | Tue | Wed | Thu | Fri | Sat |
|---|---|---|---|---|---|---|
|  |  | 1 | 2 | 3 | 4 | 5 |
| 6 | 7 | 8 | 9 | 10 | 11 | 12 |
| 13 | 14 | 15 | 16 | 17 | 18 | 19 |
| 20 | 21 | 22 | 23 | 24 | 25 | 26 |
| 27 | 28 | 29 | 30 |  |  |  |

- 11. In this exercise, you will design various classes and write a program to computerize the billing system of a hospital.
  - a. Design the class `doctorType`, inherited from the class `personType`, defined in Chapter 10, with an additional data member to store a doctor's speciality. Add appropriate constructors and member functions to initialize, access, and manipulate the data members.
  - b. Design the class `billType` with data members to store a patient's ID and a patient's hospital charges, such as pharmacy charges for medicine, doctor's fee, and room charges. Add appropriate constructors and member functions to initialize, access, and manipulate the data members.
  - c. Design the class `patientType`, inherited from the class `personType`, defined in Chapter 10, with additional data members to store a patient's ID, age, date of birth, attending physician's name, the date when the patient was admitted in the hospital, and the date when the patient was discharged from the hospital. (Use the class `dateType` to store the date of birth, admit date, discharge date, and the class `doctorType` to store the attending physician's name.) Add appropriate constructors and member functions to initialize, access, and manipulate the data members. Write a program to test your classes.

- 12. In the Programming Example Grade Report, in the definitions of the classes `courseType` and `studentType`, the accessor functions are not made constants; that is, they are not defined with the reserved word `const` at the end of their headings. Redefine these classes so that all of the accessor functions are constant functions. Accordingly, modify the definitions of the accessor functions and rerun the program.

- 13. a. Define the class `bankAccount` to store a bank customer's account number and balance. Suppose that account number is of type `int`, and balance is of type `double`. Your class should, at least, provide the following operations: set the account number, retrieve the account number, retrieve the balance, deposit and withdraw money, and print account information. Add appropriate constructors.
  - b. Every bank offers a checking account. Derive the class `checkingAccount` from the class `bankAccount` (designed in part (a)). This class inherits members to store the account number and the balance from the base class. A customer with a checking account typically receives interest, maintains a minimum balance, and pays service charges if the balance falls below the minimum balance. Add member variables to store this additional information. In addition to the operations inherited from the base class, this class should provide the following operations: set interest rate, retrieve interest rate, set minimum balance, retrieve minimum balance, set service charges, retrieve service charges, post interest, verify if the balance is less than the minimum balance, write a check, withdraw (override the method of the base class), and print account information. Add appropriate constructors.
  - c. Every bank offers a savings account. Derive the class `savingsAccount` from the class `bankAccount` (designed in part (a)). This class inherits members to store the account number and the balance from the base class. A customer with a savings account typically receives interest, makes deposits, and withdraws money. In addition to the operations inherited from the base class, this class should provide the following operations: set interest rate, retrieve interest rate, post interest, withdraw (override the method of the base class), and print account information. Add appropriate constructors.
  - d. Write a program to test your classes designed in parts (b) and (c).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_824_0.png)

## POINTERS, CLASSES, VIRTUAL FUNCTIONS, ABSTRACT CLASSES, AND LISTS

**IN THIS CHAPTER, YOU WILL:**

- Learn about the pointer data type and pointer variables
- Explore how to declare and manipulate pointer variables
- Learn about the address of operator and the dereferencing operator
- Discover dynamic variables
- Explore how to use the `new` and `delete` operators to manipulate dynamic variables
- Learn about pointer arithmetic
- Discover dynamic arrays
- Become aware of the shallow and deep copies of data
- Discover the peculiarities of classes with pointer member variables
- Learn about virtual functions
- Examine the relationship between the address of operator and classes
- Become aware of abstract classes

In Chapter 2, you learned that C++’s data types are classified into three categories: simple, structured, and pointers. Until now, you have studied only the first two data types. This chapter discusses the third data type called the pointer data type. You will first learn how to declare pointer variables (or pointers, for short) and manipulate the data to which they point. Later, you will use these concepts when you study dynamic arrays and linked lists. Linked lists are discussed in Chapter 16.

### Pointer Data Type and Pointer Variables

Chapter 2 defined a data type as a set of values together with a set of operations. Recall that the set of values is called the domain of the data type. In addition to these two properties, until now, all of the data types you have encountered have one more thing associated with them: the name of the data type. For example, there is a data type called `int`. The set of values belonging to this data type includes integers that range between −2147483648 and 2147483647, and the operations allowed on these values are the arithmetic operators described in Chapter 2. To manipulate numeric integer data in the range from −2147483648 to 2147483647, you can declare variables using the word `int`. The name of the data type allows you to declare a variable. Next, we will describe the pointer data type.

The values belonging to pointer data types are the memory addresses of your computer. As in many other languages, there is no name associated with the pointer data type in C++. Because the domain of a data type—that is, the set of values of a data type—is the addresses (memory locations), a pointer variable is a variable whose content is an address, that is, a memory location.

**Pointer variable:** A variable whose content is an address (that is, a memory address).

### Declaring Pointer Variables

As remarked previously, there is no name associated with pointer data types. Moreover, pointer variables store memory addresses. So the obvious question is: If no name is associated with a pointer data type, how do you declare pointer variables?

The value of a pointer variable is an address. That is, the value refers to another memory space. The data is typically stored in this memory space. Therefore, when you declare a pointer variable, you also specify the data type of the value to be stored in the memory location pointed to by the pointer variable.

In C++, you declare a pointer variable by using the asterisk symbol (*) between the data type and the variable name. The general syntax to declare a pointer variable is:

```cpp
dataType * identifier;
```

As an example, consider the following statements:

```cpp
int *p;
char *ch;
```
