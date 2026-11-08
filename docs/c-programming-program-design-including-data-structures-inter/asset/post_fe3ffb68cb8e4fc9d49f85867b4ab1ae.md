
figure of a class object, we will show only the member variables. As an example, Figure 10-2 shows the objects myClock and yourClock with values in their member variables.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_678_0.png)

**FIGURE 10-2** Objects myClock and yourClock

### Accessing Class Members

Once an object of a class is declared, it can access the members of the class. The general syntax for an object to access a member of a class is:

```
classObjectName.memberName
```

The class members that a class object can access depend on where the object is declared.

- If the object is declared in the definition of a member function of the class, then the object can access both the public and private members. (We will elaborate on this when we write the definition of the member function of the class `clockType` in the section “Implementation of Member Functions,” later in this chapter.)
- If the object is declared elsewhere (for example, in a user’s program), then the object can access *only* the public members of the class.

Recall that in C++, the dot, . (period), is an operator called the **member access operator**.

Example 10-1 illustrates how to access the members of a class.

**EXAMPLE 10-1**

Suppose we have the following declaration (say, in a user’s program):

```
clockType myClock;
clockType yourClock;
```

Consider the following statements:

```
myClock.setTime(5, 2, 30);
myClock.printTime();
yourClock.setTime(x, y, z);    //assume x, y, and z are
                              //variables of type int
```

### Assignment Operator and Classes

Suppose that myClock and yourClock are clockType objects, as defined previously. Furthermore, suppose that the values of myClock and yourClock are as shown in Figure 10–3(a).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_680_0.png)

**FIGURE 10-3** myClock and yourClock before and after executing the statement `myClock = yourClock`.

The statement:

```
myClock = yourClock;                 //Line 1
```

copies the value of yourClock into myClock. That is,

- the value of yourClock.hr is copied into myClock.hr,
- the value of yourClock.min is copied into myClock.min, and
- the value of yourClock.sec is copied into myClock.sec.

In other words, the values of the three member variables of yourClock are copied into the corresponding member variables of myClock. Therefore, an assignment statement performs a member-wise copy. After the statement in Line 1 executes, the values of myClock and yourClock are as shown in Figure 10–3(b).

### Class Scope

A class object can be either automatic (that is, created each time the control reaches its declaration and destroyed when the control exits the surrounding block) or static (that is, created once, when the control reaches its declaration, and destroyed when the program terminates). Also, you can declare an array of class objects. A class object has the same scope as other variables. A member of a class has the same scope as a member of a struct. That is, a member of a class is local to the class. You access a class member outside of the class by using the class object name and the member access operator (.).

### Functions and Classes

The following rules describe the relationship between functions and classes:

- Class objects can be passed as parameters to functions and returned as function values.
- As parameters to functions, class objects can be passed either by value or by reference.
- If a class object is passed by value, the contents of the member variables of the actual parameter are copied into the corresponding member variables of the formal parameter.

### Reference Parameters and Class Objects (Variables)

Recall that when a variable is passed by value, the formal parameter copies the value of the actual parameter. That is, memory space to copy the value of the actual parameter is allocated for the formal parameter. As a parameter, a class object can be passed by value.

Suppose that a class has several member variables requiring a large amount of memory to store data, and you need to pass a variable by value. The corresponding formal parameter then receives a copy of the data of the variable. That is, the compiler must allocate memory for the formal parameter, so as to copy the value of the member variables of the actual parameter. This operation might require, in addition to a large amount of storage space, a considerable amount of computer time to copy the value of the actual parameter into the formal parameter.

On the other hand, if a variable is passed by reference, the formal parameter receives only the address of the actual parameter. Therefore, an efficient way to pass a variable as a parameter is by reference. If a variable is passed by reference, then when the formal parameter changes, the actual parameter also changes. Sometimes, however, you do not want the function to be able to change the values of the member variables. In C++, you can pass a variable by reference and still prevent the function from changing its value by using the keyword const in the formal parameter declaration. As an example, consider the following function definition:

```
void testTime(const clockType& otherClock)
{
    clockType dClock;
    .
    .
    .
}
```

The function testTime contains a reference parameter, otherClock. The parameter otherClock is declared using the keyword const. Thus, in a call to the function testTime, the formal parameter otherClock receives the address of the actual parameter, but otherClock cannot modify the contents of the actual parameter. For example, after the following statement executes, the value of myClock will not be altered:

```
testTime(myClock);
```

Generally, if you want to declare a class object as a value parameter, you declare it as a reference parameter using the keyword `const`, as described previously.

Recall that if a formal parameter is a value parameter, within the function definition, you can change the value of the formal parameter. That is, you can use an assignment statement to change the value of the formal parameter (which, of course, would have no effect on the actual parameter). However, if a formal parameter is a constant reference parameter, you cannot use an assignment statement to change its value within the function, nor can you use any other function to change its value. Therefore, within the definition of the function `testTime`, you cannot alter the value of `otherClock`. For example, the following would be illegal in the definition of the function `testTime`:

```cpp
otherClock.setTime(5, 34, 56); //illegal
otherClock = dClock;           //illegal
```

### Implementation of Member Functions

When we defined the class `clockType`, we included only the function prototype for the member functions. For these functions to work properly, we must write the related algorithms. One way to implement these functions is to provide the function definition rather than the function prototype in the class itself. Unfortunately, the class definition would then be very long and difficult to comprehend. Another reason for providing function prototypes instead of function definitions relates to information hiding; that is, we want to hide the details of the operations on the data. We will discuss this issue later in this chapter, in the section “Information Hiding.”

Next, let us write the definitions of the member functions of the class `clockType`. That is, we will write the definitions of the functions `setTime`, `getTime`, `printTime`, `incrementSeconds`, `equalTime`, and so on. Because the identifiers `setTime`, `printTime`, and so forth are local to the class, we cannot reference them (directly) outside of the class. In order to reference these identifiers, we use the **scope resolution operator, ::** (double colon). In the function definition's heading, the name of the function is the name of the class, followed by the scope resolution operator, followed by the function name. For example, the definition of the function `setTime` is as follows:

```cpp
void clockType::setTime(int hours, int minutes, int seconds)
{
    if (0 <= hours && hours < 24)
        hr = hours;
    else
        hr = 0;

    if (0 <= minutes && minutes < 60)
        min = minutes;
    else
        min = 0;
```
