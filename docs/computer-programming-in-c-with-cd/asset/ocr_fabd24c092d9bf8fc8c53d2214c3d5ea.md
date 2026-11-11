The following code snippet shows the initialization of variables:

```
x = 10; // common in both C and C++
```

In the preceding code snippet, the x variable is initialized with the value 10 by using both the already discussed syntaxes to initialize a variable. The syntax to initialize and declare a variable is:

```
datatype var_name = value;
```

The following code snippet shows the valid initialization and declaration of variables:

```
int x=10; // common in both C and C++
```

In the preceding code snippet, the x variable is declared as well as initialized.

Apart from initializing variables with integer values, you can also declare variables that can store decimal values, as shown in the following code snippet:

```
float num1, num2; //declaring float variables
num1 = 5.25; //initializing float variables
num2 = num1 * 3.24;
```

In the preceding code snippet, the real variables num1 and num2 are declared and initialized.

Next, let’s discuss reference variables in C++.

# Reference Variables

A reference variable is a variable that provides a second name (alias) for an already existing variable. It may not sound appealing at first and you may question the need for creating an alias for an already existing variable. A reference variable helps you to pass values to a function by reference. Reference variables allow you to access and modify the content stored in the original variable. The syntax to create a reference variable is:

```
datatype &ref_var = var_name;
```

In the preceding syntax,

+   - datatype: Refers to the type of data the variable will hold
+   - `&ref_var`: Refers to the name of the reference variable to be declared
+   - `var_name`: Refers to the variable name whose reference variable is created

A reference variable is created by using the & symbol with the name of the reference variable. The following code snippet shows the declaration and initialization of reference variables:

```
int x=10; // x is original variable
int &a = x; // a is alias of x
```