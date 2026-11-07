
run, which contains the output of Lines 4, 5, and 6). The statement in Line 7 works as follows. In the statement:

```
student2.setFirstName("Shelly").setLastName("Malik");
```

first, the expression:

```
student2.setFirstName("Shelly")
```

is executed because the associativity of the dot operator is from left to right. This expression sets the first name to "Shelly" and returns a reference of the object, which is student2. Thus, the next expression executed is:

```
student2.setLastName("Malik")
```

which sets the last name of student2 to "Malik". The statement in Line 9 outputs the value of student2. The statement in Line 11 sets the first name of the object student3 to "Chelsea" and ignores the value returned. The statement in Line 13 outputs the value of student3. Notice the output in Line 12. The output shows only the first name, not the last name, because we have not yet set the last name of student3. The last name of student3 is still empty, which was set by the statement in Line 3 when student3 was declared. Next, the statement in Line 15 sets the last name of student3, and the statement in Line 17 outputs the value of student3.

## Friend Functions of Classes

A **friend function** of a class is a nonmember function of the class but has access to all of the members (`public` or non-`public`) of the class. To make a function be a friend to a class, the reserved word `friend` precedes the function prototype (in the class definition). The word `friend` appears only in the function prototype in the class definition, not in the definition of the friend function.

Consider the following statements:

```cpp
class classIllusFriend
{
    friend void two(/*parameters*/);
    .
    .
};
```

In the definition of the class `classIllusFriend`, `two` is declared as a `friend` of the class `classIllusFriend`. That is, it is a nonmember function of the class `classIllusFriend`. When you write the definition of the function `two`, any object of type `classIllusFriend`—which is either a local variable of `two` or a formal parameter of `two`—can access its private members within the definition of the function `two`. (Example 15-3 illustrates this concept.) Moreover, because a `friend` function is not a member of a class, its declaration can be placed within the `private`, `protected`, or `public` part of the class. However, they are typically placed before any member function declaration.

### Definition of a friend function

When writing the definition of a friend function, the name of the class and the scope resolution operator do not precede the name of the friend function in the function heading. Also, recall that the word friend does not appear in the heading of the friend function’s definition. Thus, the definition of the function two in the previous class classIllusFriend is:

```cpp
void two(/*parameters*/)
{
    .
    .
    .
}
```

Of course, we will place the definition of the friend function in the implementation file.

The next section illustrates the difference between a member function and a nonmember function (friend function) when we overload some of the operators for a specific class.

The following example shows how a friend function accesses the private members of a class.

### Example 15-3

Consider the following class:

```cpp
class classIllusFriend
{
    friend void two(classIllusFriend cIFObject);

public:
    void print();
    void setx(int a);

private:
    int x;
};
```

In the definition of the class classIllusFriend, two is declared as a friend function. Suppose that the definitions of the member functions of the class classIllusFriend are as follows:

```cpp
void classIllusFriend::print()
{
    cout << "In class classIllusFriend: x = " << x << endl;
}
```

```cpp
void classIllusFriend::setx(int a)
{
    x = a;
}
```

Consider the following definition of the function two:

```cpp
void two(classIllusFriend cIFObject)                         //Line 1
{
    classIllusFriend localTwoObject;                         //Line 2

    localTwoObject.x = 45;                                   //Line 3

    localTwoObject.print();                                  //Line 4

    cout << "Line 5: In Friend Function two "
         << "accessing private member variable "
         << "x = " << localTwoObject.x
         << endl;                                            //Line 5

    cIFObject.x = 88;                                         //Line 6

    cIFObject.print();                                        //Line 7

    cout << "Line 8: In Friend Function two "
         << "accessing private member variable "
         << "x = " << cIFObject.x << endl;                  //Line 8
}
```

The function two contains a formal parameter cIFObject and a local variable localTwoObject, both of type classIllusFriend. In the statement in Line 3, the object localTwoObject accesses its private member variable x and sets its value to 45. If two is not declared as a friend function of the class classIllusFriend, then this statement would result in a syntax error because an object cannot directly access its private members. Similarly, in the statement in Line 6, the formal parameter cIFObject accesses its private member variable x and sets its value to 88. Once again, this statement would result in a syntax error if two is not declared a friend function of the class classIllusFriend. The statement in Line 5 outputs the value of the private member variable x of localTwoObject by directly accessing x. Similarly, the statement in Line 8 outputs the value of x of cIFObject by directly accessing it. The function two also prints the value of x by using the function print (see the statements in Lines 4 and 7).

Now consider the definition of the following function main:

```cpp
int main()
{
    classIllusFriend aObject;                                //Line 9

    aObject.setx(32);                                        //Line 10

    cout << "Line 11: aObject.x: ";                         //Line 11
    aObject.print();                                         //Line 12
    cout << endl;                                            //Line 13

    cout << "*~*~*~*~* Testing Friend Function "
         << "two ~*~*~*~*~*" << endl;                       //Line 14

    two(aObject);                                            //Line 15

    return 0;
}
```

### Sample Run

```text
Line 11: aObject.x: In class classIllusFriend: x = 32

*~*~*~*~* Testing Friend Function two ~*~*~*~*~*

In class classIllusFriend: x = 45
Line 5: In Friend Function two accessing private member variable x = 45
In class classIllusFriend: x = 88
Line 8: In Friend Function two accessing private member variable x = 88
```

For the most part, the output is self-explanatory. The statement in Line 15 calls the function two (a **friend** function of the **class** classIllusFriend) and passes the object aObject as an actual parameter. Notice that the function two generates the last four lines of the output.

Later in this chapter, you will learn that for a class, stream insertion and extraction operators can be overloaded only as **friend** functions.

## Operator Functions as Member Functions and Nonmember Functions

The beginning of this chapter stated that certain rules must be followed when you include an operator function in the definition of a class. This section describes these rules.

Most operator functions can be either member functions or nonmember functions—that is, **friend** functions of a class. To make an operator function be a member or nonmember function of a class, keep the following in mind:

- 1. The function that overloads any of the operators `()`, `[]`, `->`, or `=` for a class must be declared as a member of the class.
- 2. Suppose that an operator `op` is overloaded for a class—say, `opOverClass`. (Here, `op` stands for an operator that can be overloaded, such as `+` or `>>`.)
  - a. If the far left operand of `op` is an object of a different type (that is, not of type `opOverClass`), the function that overloads the operator `op` for `opOverClass` must be a nonmember—that is, a friend of the class `opOverClass`.
  - b. If the operator function that overloads the operator `op` for the class `opOverClass` is a member of the class `opOverClass`, then when applying `op` on objects of type `opOverClass`, the far left operand of `op` must be of type `opOverClass`.
