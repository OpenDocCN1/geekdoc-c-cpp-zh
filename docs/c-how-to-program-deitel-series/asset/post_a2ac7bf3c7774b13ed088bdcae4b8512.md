
### 9.17 (Constructor Overloading)

Can a `Time` class definition that includes **both** of the following constructors:

```cpp
Time( int h = 0, int m = 0, int s = 0 );
Time();
```

be used to default construct a `Time` object? If not, explain why.

### 9.18 (Constructors and Destructors)

What happens when a return type, even void, is specified for a constructor or destructor?

### 9.19 (Date Class Modification)

Modify class `Date` in Fig. 9.17 to have the following capabilities:

- a) Output the date in multiple formats such as

```text
DDD YYYY
MM/DD/YY
June 14, 1992
```

- b) Use overloaded constructors to create `Date` objects initialized with dates of the formats in part (a).

- c) Create a `Date` constructor that reads the system date using the standard library functions of the `<ctime>` header and sets the `Date` members. See your compiler's reference documentation or en.cppreference.com/w/cpp/chrono/c for information on the functions in header `<ctime>`. You might also want to check out C++11's new chrono library at en.cppreference.com/w/cpp/chrono.

In Chapter 10, we'll be able to create operators for testing the equality of two dates and for comparing dates to determine whether one date is prior to, or after, another.

### 9.20 (SavingsAccount Class)

Create a `SavingsAccount` class. Use a static data member `annualInterestRate` to store the annual interest rate for each of the savers. Each member of the class contains a private data member `savingsBalance` indicating the amount the saver currently has on deposit. Provide member function `calculateMonthlyInterest` that calculates the monthly interest by multiplying the `savingsBalance` by `annualInterestRate` divided by 12; this interest should be added to `savingsBalance`. Provide a static member function `modifyInterestRate` that sets the static `annualInterestRate` to a new value. Write a driver program to test class `SavingsAccount`. Instantiate two different objects of class `SavingsAccount`, `saver1` and `saver2`, with balances of $2000.00 and $3000.00, respectively. Set the `annualInterestRate` to 3 percent. Then calculate the monthly interest and print the new balances for each of the savers. Then set the `annualInterestRate` to 4 percent, calculate the next month's interest and print the new balances for each of the savers.

### 9.21 (IntegerSet Class)

Create class `IntegerSet` for which each object can hold integers in the range 0 through 100. Represent the set internally as a vector of `bool` values. Element `a[i]` is true if integer `i` is in the set. Element `a[j]` is false if integer `j` is not in the set. The default constructor initializes a set to the so-called “empty set,” i.e., a set for which all elements contain false.

- a) Provide member functions for the common set operations. For example, provide a `unionOfSets` member function that creates a third set that is the set-theoretic union of two existing sets (i.e., an element of the result is set to true if that element is true in either or both of the existing sets, and an element of the result is set to false if that element is false in each of the existing sets).

- b) Provide an `intersectionOfSets` member function which creates a third set which is the set-theoretic intersection of two existing sets (i.e., an element of the result is set to false if that element is false in either or both of the existing sets, and an element of the result is set to true if that element is true in each of the existing sets).

- c) Provide an `insertElement` member function that places a new integer `k` into a set by setting `a[k]` to true. Provide a `deleteElement` member function that deletes integer `m` by setting `a[m]` to false.

![](img/b42ba5cd262b1358d16610173f975e4d_465_0.png)

- d) Provide a `printSet` member function that prints a set as a list of numbers separated by spaces. Print only those elements that are present in the set (i.e., their position in the vector has a value of true). Print `---` for an empty set.

- e) Provide an `isEqualTo` member function that determines whether two sets are equal.

- f) Provide an additional constructor that receives an array of integers and the size of that array and uses the array to initialize a set object.

Now write a driver program to test your `IntegerSet` class. Instantiate several `IntegerSet` objects. Test that all your member functions work properly.

### 9.22 (Time Class Modification)

It would be perfectly reasonable for the `Time` class of Figs. 9.4–9.5 to represent the time internally as the number of seconds since midnight rather than the three integer values hour, minute and second. Clients could use the same public methods and get the same results. Modify the `Time` class of Fig. 9.4 to implement the time as the number of seconds since midnight and show that there is no visible change in functionality to the clients of the class. [Note: This exercise nicely demonstrates the virtues of implementation hiding.]

### 9.23 (Card Shuffling and Dealing)

Create a program to shuffle and deal a deck of cards. The program should consist of class `DeckOfCards` and a driver program. Class `Card` should provide:

- a) Data members `face` and `suit` of type `int`.
- b) A constructor that receives two ints representing the face and suit and uses them to initialize the data members.
- c) Two static arrays of strings representing the faces and suits.
- d) A `toString` function that returns the `Card` as a string in the form “face of suit.” You can use the `+` operator to concatenate strings.

Class `DeckOfCards` should contain:

- a) An array of Cards named `deck` to store the Cards.
- b) An integer `currentCard` representing the next card to deal.
- c) A default constructor that initializes the Cards in the deck.
- d) A `shuffle` function that shuffles the Cards in the deck. The shuffle algorithm should iterate through the array of Cards. For each Card, randomly select another Card in the deck and swap the two Cards.
- e) A `dealCard` function that returns the next Card object from the deck.
- f) A `moreCards` function that returns a bool value indicating whether there are more Cards to deal.

The driver program should create a `DeckOfCards` object, shuffle the cards, then deal the 52 cards.

### 9.24 (Card Shuffling and Dealing)

Modify the program you developed in Exercise 9.23 so that it deals a five-card poker hand. Then write functions to accomplish each of the following:

- a) Determine whether the hand contains a pair.
- b) Determine whether the hand contains two pairs.
- c) Determine whether the hand contains three of a kind (e.g., three jacks).
- d) Determine whether the hand contains four of a kind (e.g., four aces).
- e) Determine whether the hand contains a flush (i.e., all five cards of the same suit).
- f) Determine whether the hand contains a straight (i.e., five cards of consecutive face values).

### 9.25 (Project: Card Shuffling and Dealing)

Use the functions from Exercise 9.24 to write a program that deals two five-card poker hands, evaluates each hand and determines which is the better hand.

### 9.26 (Project: Card Shuffling and Dealing)

Modify the program you developed in Exercise 9.25 so that it can simulate the dealer. The dealer’s five-card hand is dealt “face down” so the player can-

![](img/b42ba5cd262b1358d16610173f975e4d_469_0.png)

- **10.1** Introduction
- **10.2** Using the Overloaded Operators of Standard Library Class `string`
- **10.3** Fundamentals of Operator Overloading
- **10.4** Overloading Binary Operators
- **10.5** Overloading the Binary Stream Insertion and Stream Extraction Operators
- **10.6** Overloading Unary Operators
- **10.7** Overloading the Unary Prefix and Postfix `++` and `--` Operators
- **10.8** Case Study: A Date Class
- **10.9** Dynamic Memory Management
- **10.10** Case Study: Array Class
  - 10.10.1 Using the Array Class
  - 10.10.2 Array Class Definition
- **10.11** Operators as Member vs. Non-Member Functions
- **10.12** Converting Between Types
- **10.13** `explicit` Constructors and Conversion Operators
- **10.14** Overloading the Function Call Operator `()`
- **10.15** Wrap-Up

*Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises*

## 10.1 Introduction

This chapter shows how to enable C++’s operators to work with class objects—a process called **operator overloading**. One example of an overloaded operator built into C++ is `<<`, which is used both as the stream insertion operator and as the bitwise left-shift operator (which is discussed in Chapter 22). Similarly, `>>` also is overloaded; it’s used both as the stream extraction operator and the bitwise right-shift operator. Both of these operators are overloaded in the C++ Standard Library. You’ve been using overloaded operators since early in the book. The overloads are built into the base C++ language itself. For example, C++ overloads the addition operator (`+`) and the subtraction operator (`-`) to perform differently, depending on their context in integer, floating-point and pointer arithmetic with data of fundamental types.

You can overload *most* operators to be used with class objects—the compiler generates the appropriate code based on the *types* of the operands. The jobs performed by overloaded operators also can be performed by explicit function calls, but operator notation is often more natural.

Our examples start by demonstrating the C++ Standard Library’s class `string`, which has lots of overloaded operators. This enables you to see overloaded operators in use before implementing your own overloaded operators. Next, we create a `PhoneNumber` class that enables us to use overloaded operators `<<` and `>>` to conveniently output and input fully formatted, 10-digit phone numbers. We then present a `Date` class that overloads the prefix and postfix increment (`++`) operators to add one day to the value of a `Date`. The class also overloads the `+=` operator to allow a program to increment a `Date` by the number of days specified on the right side of the operator.

Next, we present a capstone case study—an `Array` class that uses overloaded operators and other capabilities to solve various problems with pointer-based arrays. This is one of the most important case studies in the book. Many of our students have indicated that the `Array` case study is their “light bulb moment” in truly understanding what classes and object technology are all about. As part of this class, we’ll overload stream insertion, stream extraction, assignment, equality, relational and subscript operators. Once you master this
