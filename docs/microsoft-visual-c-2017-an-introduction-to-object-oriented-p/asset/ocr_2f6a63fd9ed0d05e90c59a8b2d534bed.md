You declare all variables you want to use in a program. A variable declaration is the statement that names a variable and reserves storage for it. A declaration includes the following:

+   - The data type that the variable will store
- The variable's name (its identifier)
- An assignment operator and assigned value when you want a variable to contain an initial value
- An ending semicolon.

For example, the following statement declares a variable of int myAge and assigns it an initial value of 25:

```
int myAge = 25;
```

The int type represents integer, which is a whole number. Complete discussion of this data type appears in the section "Using the Integral Data Types" later in this chapter. The equal sign (=) is the assignment operator; any value to the right of the assignment operator is assigned to the identifier to the left. An assignment when a variable is declared is an initialization; an assignment made to left is an assignment. Thus, the statement initializes myAge to 25:

```
int myAge = 25;
```

A statement such as the following assigns a new value to the variable:

```
myAge = 42;
```

Notice that the data type is not used when an assignment is made; it is only used in a declaration.

Also note that the expression 25 = myAge; is illegal because assignment always takes place from right to left. By definition, a literal constant cannot be altered, so it is illegal to place one (such as 25) on the left side of an assignment operator. The assignment operator means "is the value of the following expression.\ In other words, the statement myAge = 25; can be read as "myAge is assigned the value of the following expression"

Instead of using a name from the Type column of Table 2-1, you could use the fully qualified name that listed in the System column. For example, instead of using the name int, you can use the full name System.Int32 (The number 32 in the name System.Int32 represents the number of bits of storage allowed for the variable. There are eight bits in a byte, and an int occupies four bytes). It's better to use the shorter alias int, however, for the following reasons:

+   - The shorter alias is easier to read.
- The shorter alias resembles names used in other languages such as Java and C++.
- Other C# programmers expect the shorter names.