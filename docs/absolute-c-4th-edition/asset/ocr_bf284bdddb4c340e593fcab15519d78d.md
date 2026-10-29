# Pitfall UNINITIALIZED VARIABLES

A variable has no meaningful value until a program gives it one. For example, if the variable minimumNumber has not been given a value either as the left-hand side of an assignment statement or by some other means (such as being given an input value with a cin statement), then the following is an error:

```
desiredNumber = minimumNumber + 10;
```

This is because minimumNumber has no meaningful value, and so the entire expression on the right-hand side of the equal sign has no meaningful value. A variable like minimumNumber that has not been given a value is said to be uninitialized. This situation is, in fact, worse than it would be if minimumNumber had no value at all. An uninitialized variable, like minimumNumber, will simply have some garbage value. The value of an uninitialized variable is determined by whatever pattern of zeros and ones was left in its memory location by the last program that used that portion of memory.

One way to avoid an uninitialized variable is to initialize variables at the same time they are declared. This can be done by adding an equal sign and a value, as follows:

```
int minimumNumber = 3;
```

This both declares minimumNumber to be a variable of type int and sets the value of the variable minimumNumber equal to 3. You can use a more complicated expression involving operations such as addition or multiplication when you initialize a variable inside the declaration in this way. As another example, the following declares three variables and initializes two of them:

```
double rate = 0.07, time, balance = 0.00;
```

C++ allows an alternative notation for initializing variables when they are declared. This alternative notation is illustrated by the following, which is equivalent to the preceding declaration:

```
double rate(0.07), time, balance(0.00);
```

# INITIALIZING VARIABLES IN DECLARATIONS

You can initialize a variable (that is, give it a value) at the time that you declare the variable.

# SYNTAX

```
Type_Name Variable_Name_1 = Expression_for_Value_1,
    Variable_Name_2 = Expression_for_Value_2, ...;
```