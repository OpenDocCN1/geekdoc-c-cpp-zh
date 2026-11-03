```
```
#define name value
```
```

Here 'name' is the symbolic name for the constant, and is generally written in uppercase letters. 'value' can be numeric, character or string constant.

Some examples of symbolic constants are-

```
```
#define MAX 100
#define PI 3.14159625
#define CH 'y'
#define NAME "Suresh"
```
```

In the program, these names will be replaced by the corresponding values. These symbolic constants improve the readability and modifiability of the program.

# ## 2.9 Variables

Variable is a name that can be used to store values. Variables can take different values but one at a time. These values can be changed during execution of the program. A data type is associated with each variable. The data type of the variable decides what values it can take. The rules for naming variables are same as that for naming identifiers.

# ### 2.9.1 Declaration of Variables

It is must to declare a variable before it is used in the program. Declaration of a variable specifies its name and datatype. The type and range of values that a variable can store depends upon its datatype. The syntax of declaration of a variable is-

```
```
datatype variablename;
```
```

Here datatype may be int, float, char, double etc. Some examples of declaration of variables are-

```
```
int x;
float salary;
char grade;
```
```

Here x is a variable of type int, salary is a variable of type float, and grade is a variable of type char. We can also declare more than one variable in a single declaration. For example-

```
```
int x, y, z, total;
```
```

Here x, y, z, total are all variables of type int.

# ### 2.9.2 Initialisation of Variables

When a variable is declared it contains undefined value commonly known as garbage value. If we want we can assign some initial value to the variable during the declaration itself, this is called initialisation of the variable. For example-

```
```
int a = 5;
float x = 8.9, y = 10.5;
char ch = 'y';
double num = 0.15197e-7;
int l, m, n, total = 0;
```
```

In the last declaration only variable total has been initialised.