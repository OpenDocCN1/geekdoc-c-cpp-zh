# Representing Numbers

# Scientific notation

You may represent very large numbers using scientific notation:

```
3.95e8
```

e8 represents 10 to the power 8. Thus, 3.95e8 is equal to 3.95 times 10⁸—that is, 395,000,000.

Similarly, 3.95e-8 represents 3.95 times 10 to the power -8—that is, 0.0000000395.

Numbers can have only numeric digits, decimal point, minus and plus signs, and the letter “e” or “E” when using scientific notation. Commas and dollar signs ($) are invalid within a number. So, the following statements are invalid:

```
double unitPrice = $1.50;    //Invalid; dollar sign is not allowed in a number
double cost = 3,520.00;      //Invalid; comma is not allowed in a number
double amount = "15.45";   //Invalid; "15.45" is a string
```

Caution! In general, the compiler does not like it when you assign the wrong type of value to a variable. The following statement would result in an error because scoops is declared as type int, which is a type of integer, but 1.5 is a real number.

```
int scoops = 1.5    //Invalid; 1.5 is not an integer
```

We will look at specific rules on mixing different types of integer and real types in Chapter 2.

# Assigning the Value of One Variable to Another Variable

You may assign the value of one variable to another variable, as in the following example:

```
int scoops = 3;
int temp;
temp = scoops;
```

The statement “temp = scoops” copies the value of scoops into the variable temp. After execution of this statement, the storage locations for both variables will contain the same value 3:

![](bbox=[0.11, 0.975, 0.42, 1.05])

What happens if you change the value of scoops by adding the following statement after the above code?

```
scoops = 5;
```

Does it change the value of temp? The answer is no, because each variable has its own storage location. After execution of the statement “scoops = 5,” the two variables will have the following values:

![](bbox=[0.11, 1.25, 0.42, 1.325])