
# TIP: Use Hierarchical Structures

Sometimes it makes sense to have structures whose members are themselves smaller structures. For example, a structure type called PersonInfo that can be used to store a person's height, weight, and birth date can be defined as follows:

```
struct Date
{
    int month;
    int day;
    int year;
};
```

```
struct PersonInfo
{
    double height; //in inches
    int weight; //in pounds
    Date birthday;
};
```

A structure variable of type PersonInfo is declared in the usual way:

```
PersonInfo person1;
```

If the structure variable person1 has had its value set to record a person's birth date, then the year the person was born can be output to the screen as follows:

```
cout << person1.birthday.year;
```

The way to read such expressions is left to right, and very carefully. Starting at the left end, person1 is a structure variable of type PersonInfo. To obtain the member variable with the name birthday, you use the dot operator as follows:

```
person1.birthday
```

This member variable is itself a structure variable of type Date. Thus, this member variable itself has member variables. A member variable of the structure variable person1.birthday is obtained by adding a dot and the member variable name, such as year, which produces the expression person1.birthday.year shown previously.

In Display 6.2 we have rewritten the class for a certificate of deposit from Display 6.1. This new version has a member variable of the structure type Date that holds the date of maturity. We have also replaced the single balance member variable with two new member variables giving the initial balance and the balance at maturity.

# Display 6.2   A Structure with a Structure Member (part 1 of 2)

```
//Program to demonstrate the CDAccount structure type.
#include <iostream>
using namespace std;

struct Date
{
    int month;
    int day;
    int year;
};

//Improved structure for a bank certificate of deposit:
struct CDAccount
{
    double initialBalance;
    double interestRate;
    int term; //months until maturity
    Date maturity; //date when CD matures
    double balanceAtMaturity;
};

void getCDData(CDAccount& theAccount);
//Postcondition: theAccount.initialBalance, theAccount.interestRate,
//theAccount.term, and theAccount.maturity have been given values
//that the user entered at the keyboard.

void getDate(Date& theDate);
//Postcondition: theDate.month, theDate.day, and theDate.year
//have been given values that the user entered at the keyboard.

int main( )
{
    CDAccount account;
    cout << "Enter account data on the day account was opened:\n";
    getCDData(account);
    double rateFraction, interest;
    rateFraction = account.interestRate / 100.0;
    interest = account.initialBalance * (rateFraction*(account.term /
                                                        12.0));
    account.balanceAtMaturity = account.initialBalance + interest;

    cout.setf(ios::fixed);
    cout.setf(ios::showpoint);
    cout.precision(2);
    cout << "When the CD matured on "
         << account.maturity.month << "/" << account.maturity.day
         << "," << account.maturity.year << " it had
         << "a balance of $"
         << account.balanceAtMaturity << endl;
    return 0;
}
```

![](img/c76bba8c1d927f399768ffe2ab5f5bee_282_0.png)

# Display 6.2 A Structure with a Structure Member (part 2 of 2)

```
45 }
46 //uses iostream:
47 void getCDData(CDAccount& theAccount)
48 {
49   cout << "Enter account initial balance: $";
50   cin >> theAccount.initialBalance;
51   cout << "Enter account interest rate: ";
52   cin >> theAccount.interestRate;
53   cout << "Enter the number of months until maturity: ";
54   cin >> theAccount.term;
55   cout << "Enter the maturity date:\n";
56   getDate(theAccount.maturity);
57 }
```

```
58 //uses iostream
59 void getDate(Date& theDate)
60 {
61   cout << "Enter month: ";
62   cin >> theDate.month;
63   cout << "Enter day: ";
64   cin >> theDate.day;
65   cout << "Enter year: ";
66   cin >> theDate.year;
67 }
```

# Sample Dialogue

```
Enter account data on the day account was opened:
Enter account initial balance: $100.00
Enter account interest rate: 10.0
Enter the number of months until maturity: 6
Enter the maturity date:
Enter month: 2
Enter day: 14
Enter year: 1899
When the CD matured on 2-14-1899
it had a balance of $105.00
```

# Initializing Structures

You can initialize a structure at the time that it is declared. To give a structure variable a value, follow it by an equal sign and a list of the member values enclosed in braces. For example, the following definition of a structure type for a date was given in the previous subsection:

```
struct Date
{
  int month;
```

int day;
int year;
};

Once the type Date is defined, you can declare and initialize a structure variable called dueDate as follows:

```
Date dueDate = {12, 31, 2012};
```

The initializing values must be given in the order that corresponds to the order of member variables in the structure-type definition. In this example, dueDate.month receives the first initializing value of 12, dueDate.day receives the second value of 31, and dueDate.year receives the third value of 2012.

It is an error if there are more initializer values than struct members. If there are fewer initializer values than struct members, the provided values are used to initialize data members, in order. Each data member without an initializer is initialized to a zero value of an appropriate type for the member.

# Self-Test Exercises

+   1. Given the following structure and structure variable declaration:
+   
+   ```cpp
+   struct CDAccountV2
+   {
+       double balance;
+       double interestRate;
+       int term;
+       char initial1;
+       char initial2;
+   };
+   CDAccountV2 account;
+   ```
+   
+   What is the type of each of the following? Mark any that are not correct.
+   
+   a. `account.balance`
+   b. `account.interestRate`
+   c. `CDAccountV1.term`
+   d. `account.initial2`
+   e. `account`

+   2. Consider the following type definition:
+   
+   ```cpp
+   struct ShoeType
+   {
+       char style;
+       double price;
+   };
+   ```

# Self-Test Exercises (continued)

Given the previous structure-type definitions, what will be the output produced by the following code?

```
ShoeType shoe1, shoe2;
shoe1.style = 'A';
shoe1.price = 9.99;
cout << shoe1.style << " $" << shoe1.price << endl;
shoe2 = shoe1;

shoe2.price = shoe2.price/9;
cout << shoe2.style << " $" << shoe2.price << endl;
```

3. What is the error in the following structure definition?

```
struct Stuff
{
    int b;
    int c;
}

int main( )
{
    Stuff x;
    // other code
}
```

4. Given the following struct definition:

```
struct A
{
    int b;
    int c;
};
```

declare x to have this structure type. Initialize the members of x, member b and member c, to the values 1 and 2, respectively.

5. Here is an initialization of a structure type. State what happens with each initialization. Note any problems with these initializations.

```
struct Date
{
    int month;
    int day;
    int year;
};
```

a. Date dueDate = {12, 21};
b. Date dueDate = {12, 21, 1995};
c. Date dueDate = {12, 21, 19, 95};

# Self-Test Exercises (continued)

6. Write a definition for a structure type for records consisting of a person’s wage rate, accrued vacation (which is some whole number of days), and status (which is either hourly or salaried). Represent the status as one of the two char values ‘H’ and ‘S’. Call the type EmployeeRecord.

7. Give a function definition corresponding to the following function declaration. (The type ShoeType is given in Self-Test Exercise 2.)

void readShoeRecord(ShoeType& newShoe);
//Fills newShoe with values read from the keyboard.

8. Give a function definition corresponding to the following function declaration. (The type ShoeType is given in Self-Test Exercise 2.)

ShoeType discount(ShoeType oldRecord);
//Returns a structure that is the same as its argument,
//but with the price reduced by 10%.

# 6.2 Classes

> We all know—the Times knows—but we pretend we don’t.

> VIRGINIA WOOLF, “An Unwritten Novel,” Monday or Tuesday. New York: Harcourt, Brace, and Company, Inc., 1921

A class is basically a structure with member functions as well as member data. Classes are central to the programming methodology known as object-oriented programming.

# Defining Classes and Member Functions

class A class is a type that is similar to a structure type, but a class type normally has member functions as well as member variables. An overly simple, but illustrative, example of a class called DayOfYear is given in Display 6.3. This class has one member function named output, as well as the two member variables month and day. The term public is called an access specifier. It simply means that there are no restrictions on the members that follow. We will discuss public, and its alternatives after going through this simple example. The type DayOfYear defined in Display 6.3 is a class definition for objects whose values are dates, such as January 1 or July 4.

object The value of a variable of a class type is called an object (therefore, when speaking loosely, a variable of a class type is also often called an object). An object has both data members and function members. When programming with classes, a program is viewed as a collection of interacting objects. The objects can interact because they are capable of actions, namely, invocations of member functions. Variables of a class type hold objects as values. Variables of a class type are declared in the same way as variables of the predefined types and in the same way as structure variables.
