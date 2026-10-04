# Chapter 6 361

# Point of Information

# Storage Categories

Variables of type auto and register are always local variables. Only non-static global variables can be declared by using the extern keyword. Doing so extends the variable's scope into another file or function.

Making a global static makes the variable to the file in which it's declared. static variables cannot use the extern keyword. Except for static variables, all variables are initialized each time they come into scope; static variables are initialized only once, when they're defined

variable already exists and can be used. The actual storage for the variable must be somewhere else in the program by using one, and only one, global declaration statement in which the extern has not been used. The global variable can, of course, be initialized in its original declaration. Initialization in an extern declaration statement is not allowed, and causes a compilation error.

The existence of the extern storage category is the reason for carefully distinguishing between the creation and declaration of a variable. Declaration statements containing the extern word do not create storage areas; they only extend the scope of global variables

The last global storage category, static, is to prevent extending a global variable into a second file. Global static variables are declared in the same way as local static variables, except the declaration statement is placed outside any function.

The scope of a global static variable can't be extended beyond the file in which it's declared. Because they are "known" and can be used only in the file where they are declared, other files can access or change their values. Therefore, global static variables can't subsequently be extended to a second file by using an extern declaration statement. Trying to do so results in a compilation error.

# EXERCISES 6.6

+   1. (Practice) a. List the storage categories available to local variables.
b. List the storage categories available to global variables.

+   2. (Practice) Describe the difference between a local auto variable and a local static variable.

+   3. (Practice) What is the difference between the following functions?

```
void initi() {
  static int yrs = 1;
```