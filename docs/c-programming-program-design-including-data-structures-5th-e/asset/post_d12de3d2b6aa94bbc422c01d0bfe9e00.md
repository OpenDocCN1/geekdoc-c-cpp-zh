
figure of a class object, we will show only the member variables. As an example, Figure 11-2 shows the objects myClock and yourClock with values in their member variables.

![](img/f97f778697507bb6fdd80c5991210cba_648_0.png)

FIGURE 11-2 Objects myClock and yourClock

## Accessing Class Members

Once an object of a class is declared, it can access the members of the class. The general syntax for an object to access a member of the class is:

```
classObjectName.memberName
```

The class members that a class object can access depend on where the object is declared.

- If the object is declared in the definition of a member function of the class, then the object can access both the public and private members. (We will elaborate on this when we write the definition of the member function equalTime of the class clockType in the section "Implementation of Member Functions," later in this chapter.)
- If the object is declared elsewhere (for example, in a user's program), then the object can access only the public members of the class.

Recall that in C++, the dot, . (period), is an operator called the member access operator. Example 11-1 illustrates how to access the members of a class.

### EXAMPLE 11-1

Suppose we have the following declaration (say, in a user's program):

```
clockType myClock;
clockType yourClock;
```

Consider the following statements:

```cpp
myClock.setTime(5, 2, 30);
myClock.printTime();
yourClock.setTime(x, y, z);    //assume x, y, and z are
                              //variables of type int
if (myClock.equalTime(yourClock))
.
.
.
```

These statements are legal; that is, they are syntactically correct.

In the first statement, `myClock.setTime(5, 2, 30);`, the member function `setTime` is executed. The values 5, 2, and 30 are passed as parameters to the function `setTime`, and the function uses these values to set the values of the three member variables `hr`, `min`, and `sec` of `myClock` to 5, 2, and 30, respectively. Similarly, the second statement executes the member function `printTime` and outputs the contents of the three member variables of `myClock`. In the third statement, the values of the variables `x`, `y`, and `z` are used to set the values of the three member variables of `yourClock`.

In the fourth statement, the member function `equalTime` executes and compares the three member variables of `myClock` to the corresponding member variables of `yourClock`. Because in this statement `equalTime` is a member of the object `myClock`, it has direct access to the three member variables of `myClock`. So it needs one more object, which in this case is `yourClock`, to compare. This explains why the function `equalTime` has only one parameter.

The objects `myClock` and `yourClock` can access only **public** members of the class. Thus, the following statements are illegal because `hr` and `min` are declared as **private** members of the `class` `clockType`, and hence, cannot be accessed by the objects `myClock` and `yourClock`:

```cpp
myClock.hr = 10;           //illegal
myClock.min = yourClock.min; //illegal
```

### Built-in Operations on Classes

Most of C++’s built-in operations do not apply to classes. You cannot use arithmetic operators to perform arithmetic operations on class objects (unless they are overloaded; see Chapter 14). For example, you cannot use the operator + to add two class objects of, say, type `clockType`. Also, you cannot use relational operators to compare two class objects for equality (unless they are overloaded; see Chapter 14).

The two built-in operations that are valid for class objects are member access (.) and assignment (=). You have seen how to access an individual member of a class by using the name of the class object, then a dot, and then the member name. (For example, if `myClock` is a `clockType` object, in the statement `myClock.incrementSeconds();`, `myClock` accesses the member `incrementSeconds`.)

We now show how an assignment statement works with the help of an example.

### Assignment Operator and Classes

Suppose that myClock and yourClock are clockType objects, as defined previously. Furthermore, suppose that the values of myClock and yourClock are as shown in Figure 11-3(a).

![](img/f97f778697507bb6fdd80c5991210cba_650_0.png)

**FIGURE 11-3** myClock and yourClock before and after executing the statement myClock = yourClock;

The statement:

```cpp
myClock = yourClock;        //Line 1
```

copies the value of yourClock into myClock. That is,

- the value of yourClock.hr is copied into myClock.hr,
- the value of yourClock.min is copied into myClock.min, and
- the value of yourClock.sec is copied into myClock.sec.

In other words, the values of the three member variables of yourClock are copied into the corresponding member variables of myClock. Therefore, an assignment statement performs a member-wise copy. After the statement in Line 1 executes, the values of myClock and yourClock are as shown in Figure 11-3(b).

### Class Scope

A class object can be either automatic (that is, created each time the control reaches its declaration and destroyed when the control exits the surrounding block) or static (that is, created once, when the control reaches its declaration, and destroyed when the program terminates). Also, you can declare an array of class objects. A class object has the same scope as other variables. A member of a class has the same scope as a member of a struct. That is, a member of a class is local to the class. You access a class member outside of the class by using the class object name and the member access operator (.).

## Functions and Classes

The following rules describe the relationship between functions and classes:

- Class objects can be passed as parameters to functions and returned as function values.
- As parameters to functions, class objects can be passed either by value or by reference.
- If a class object is passed by value, the contents of the member variables of the actual parameter are copied into the corresponding member variables of the formal parameter.

### Reference Parameters and Class Objects (Variables)

Recall that when a variable is passed by value, the formal parameter copies the value of the actual parameter. That is, memory space to copy the value of the actual parameter is allocated for the formal parameter. As a parameter, a class object can be passed by value.

Suppose that a class has several member variables requiring a large amount of memory to store data, and you need to pass a variable by value. The corresponding formal parameter then receives a copy of the data of the variable. That is, the compiler must allocate memory for the formal parameter, so as to copy the value of the member variables of the actual parameter. This operation might require, in addition to a large amount of storage space, a considerable amount of computer time to copy the value of the actual parameter into the formal parameter.

On the other hand, if a variable is passed by reference, the formal parameter receives only the address of the actual parameter. Therefore, an efficient way to pass a variable as a parameter is by reference. If a variable is passed by reference, then when the formal parameter changes, the actual parameter also changes. Sometimes, however, you do not want the function to be able to change the values of the member variables. In C++, you can pass a variable by reference and still prevent the function from changing its value by using the keyword const in the formal parameter declaration. As an example, consider the following function definition:

```cpp
void testTime(const clockType& otherClock)
{
    clockType dClock;
    .
    .
    .
}
```

The function testTime contains a reference parameter, otherClock. The parameter otherClock is declared using the keyword const. Thus, in a call to the function testTime, the formal parameter otherClock receives the address of the actual parameter, but otherClock cannot modify the contents of the actual parameter. For example, after the following statement executes, the value of myClock will not be altered:

```cpp
testTime(myClock);
```
