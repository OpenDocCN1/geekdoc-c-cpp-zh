
In C++, `class` is a reserved word, and it defines only a data type; no memory is allocated. It announces the declaration of a class. Moreover, note the semicolon (`;`) after the right brace. The semicolon is part of the syntax. A missing semicolon, therefore, will result in a syntax error.

The members of a `class` are classified into three categories: `private`, `public`, and `protected`. This chapter mainly discusses the first two types, `private` and `public`.

In C++, `private`, `protected`, and `public` are reserved words and are called member access specifiers.

Following are some facts about `public` and `private` members of a class:

- By default, all members of a class are `private`.
- If a member of a class is `private`, you cannot access it outside of the class. (Example 11-1 illustrates this concept.)
- A `public` member is accessible outside of the class. (Example 11-1 illustrates this concept.)
- To make a member of a class `public`, you use the member access specifier `public` with a colon, `:`

Suppose that we want to define a class to implement the time of day in a program. Because a clock gives the time of day, let us call this class `clockType`. Furthermore, to represent time in computer memory, we use three `int` variables: one to represent the hours, one to represent the minutes, and one to represent the seconds.

Suppose these three variables are:

```cpp
int hr;
int min;
int sec;
```

We also want to perform the following operations on the time:

- 1. Set the time.
- 2. Retrieve the time.
- 3. Print the time.
- 4. Increment the time by one second.
- 5. Increment the time by one minute.
- 6. Increment the time by one hour.
- 7. Compare the two times for equality.

To implement these seven operations, we will write seven functions—`setTime`, `getTime`, `printTime`, `incrementSeconds`, `incrementMinutes`, `incrementHours`, and `equalTime`.

From this discussion, it is clear that the class `clockType` has 10 members: three member variables and seven member functions.

![](img/f97f778697507bb6fdd80c5991210cba_644_0.png)

Some members of the class `clockType` will be **private**; others will be **public**. Deciding which member to make **public** and which to make **private** depends on the nature of the member. The general rule is that any member that needs to be accessed outside of the class is declared **public**; any member that should not be accessed directly by the user should be declared **private**. For example, the user should be able to set the time and print the time. Therefore, the members that set the time and print the time should be declared **public**.

Similarly, the members to increment the time and compare the time for equality should be declared **public**. On the other hand, to prevent the direct manipulation of the member variables `hr`, `min`, and `sec`, we will declare them **private**. Furthermore, note that if the user has direct access to the member variables, member functions such as `setTime` are not needed. The second part of this chapter (beginning with the section “Information Hiding”) explains why some members need to be **public** and others should be **private**.

The following statements define the class `clockType`:

```cpp
class clockType
{
public:
    void setTime(int, int, int);
    void getTime(int&, int&, int&) const;
    void printTime() const;
    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();
    bool equalTime(const clockType&) const;

private:
    int hr;
    int min;
    int sec;
};
```

In this definition:

- The class `clockType` has seven member functions: `setTime`, `getTime`, `printTime`, `incrementSeconds`, `incrementMinutes`, `incrementHours`, and `equalTime`. It has three member variables: `hr`, `min`, and `sec`.
- The three member variables—`hr`, `min`, and `sec`—are **private** to the class and cannot be accessed outside of the class. (Example 11-1 illustrates this concept.)
- The seven member functions—`setTime`, `getTime`, `printTime`, `incrementSeconds`, `incrementMinutes`, `incrementHours`, and `equalTime`—can directly access the member variables (`hr`, `min`, and `sec`). In other words, when we write the definitions of these functions, we do not pass these member variables as parameters to the member functions.
- In the function `equalTime`, the formal parameter is a constant reference parameter. That is, in a call to the function `equalTime`, the formal parameter receives the address of the actual parameter, but the formal parameter cannot modify the value of the actual parameter. You could have declared the formal parameter as a value parameter, but that would require the formal parameter to copy the value of the actual parameter, which could result in poor performance. (See the section “Reference Parameters and Class Objects (Variables)” in this chapter for an explanation.)
- The word `const` at the end of the member functions `getTime`, `printTime`, and `equalTime` specifies that these functions cannot modify the member variables of a variable of type `clockType`.

> **NOTE**  
> The `private` and `public` members can appear in any order. If you want, you can declare the `private` members first and then declare the `public` ones. The section “Order of public and private Members of a Class” in this chapter discusses this issue.

> **NOTE**  
> In the definition of the class `clockType`, all member variables are `private` and all member functions are `public`. However, a member function can also be `private`. For example, if a member function is used only to implement other member functions of the class and the user does not need to access this function, you make it `private`. Similarly, a member variable of a class can also be `public`.

Note that we have not yet written the definitions of the member functions of the class. You will learn how to write them shortly.

The function `setTime` sets the three member variables—`hr`, `min`, and `sec`—to a given value. The given values are passed as parameters to the function `setTime`. The function `printTime` prints the time, that is, the values of `hr`, `min`, and `sec`. The function `incrementSeconds` increments the time by one second, the function `incrementMinutes` increments the time by one minute, the function `incrementHours` increments the time by one hour, and the function `equalTime` compares two times for equality.

Note that the function `equalTime` has only one parameter, although you need two things to make a comparison. We will explain this point with the help of an example in the section “Implementation of Member Functions,” later in this chapter.

## Unified Modeling Language Class Diagrams

A class and its members can be described graphically using a notation known as the **Unified Modeling Language** (UML) notation. For example, Figure 11-1 shows the UML class diagram of the class `clockType`.

![](img/f97f778697507bb6fdd80c5991210cba_647_0.png)

FIGURE 11-1 UML class diagram of the class clockType

The top box contains the name of the class. The middle box contains the member variables and their data types. The last box contains the member function name, parameter list, and the return type of the function. A + (plus) sign in front of a member name indicates that this member is a public member; a - (minus) sign indicates that this is a private member. The symbol # before the member name indicates that the member is a protected member.

## Variable (Object) Declaration

Once a class is defined, you can declare variables of that type. In C++ terminology, a class variable is called a **class object** or **class instance**. To help you become familiar with this terminology, from now on we will use the term class object, or simply **object**, for a class variable.

The syntax for declaring a class object is the same as that for declaring any other variable. The following statements declare two objects of type `clockType`:

```cpp
clockType myClock;
clockType yourClock;
```

Each object has 10 members: seven member functions and three member variables. Each object has separate memory allocated for **hr**, **min**, and **sec**.

In actuality, memory is allocated only for the member variables of each class object. The C++ compiler generates only one physical copy of a member function of a class, and each class object executes the same copy of the member function. Therefore, whenever we draw the
