# Rules to Name a Variable

+   1. Variable name must not start with a digit.
2. Variable name can consist of alphabets, digits and special symbols underscore_
3. Blank or spaces are not allowed in variable name.
4. Keywords are not allowed as variable name.
5. Upper and lower case names are treated as different, as C is case-sensitive, so it is suggested to keep the variable names in lower case.

# Declaring, Defining and Initializing a Variable

Declaration of variables must be done before they are used in the program. Declaration does the following things:

+   1. It tells the compiler what the variable name is.
2. It specifies what type of data the variable will hold.
3. Until the variable is defined the compiler doesn't have to worry about allocating memory space to the variable.
4. Declaration is like informing the compiler that there exist a variable with following data type which is used in the program.
5. A variable is declared using the extern keyword, outside the main() function.

```
extern int a;
extern float b;
extern double c, d;
```

Defining a variable means the compiler has to now assign to a storage to the variable because it will be used in the program. It is not necessary to declare a variable using extern keyword, if you want to use it in your program. You can directly define a variable inside the main() function and use it.

To define a function we must provide the data type and the variable name. We can even define multiple variables of same data type in a single line by using comma to separate them.

```
int a;
floatab,e;
```

Initializing a variable means to provide it with a value. A variable can be initialized and defined in a single statement, like:

```
int a=5;
```