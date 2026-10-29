A sample run of Program 4.2 follows.

```
Enter the temperature to be converted: 212
Enter an f if the temperature is in Fahrenheit
    or a c if the temperature is in Celsius: f

The equivalent Celsius temperature is 100.00
```

# Block Scope

All statements contained in a compound statement constitute a single block of code, and any variable declared in this block has meaning only between its declaration and the closing braces defining the block. For example, take a look at the following example, which consists of two blocks of code:

```
{  // start of outer block
    int a = 25;
    int b = 17;
    cout << "The value of a is " << a
         << " and b is " << b << endl;

    {  // start of inner block
        double a = 46.25;
        int c = 10;
        cout << "a is now " << a
             << " b is now " << b
             << " and c is " << c << endl;
    }  // end of inner block

    cout << "a is now " << a << " and b is " << b << endl;
}  // end of outer block
```

This section of code produces the following output:

```
The value of a is 25 and b is 17
a is now 46.25 b is now 17 and c is 10
a is now 25 and b is 17
```

This output is produced as follows: The first block of code defines two variables named a and b, which can be used anywhere in this block after their declarations, including any block inside this outer block. In the inner block, two new variables have been declared, named a and c. Therefore, at this stage, four different variables have been created, two with the same name. When a variable is referenced, the compiler first attempts to access a variable with the correct name that has been declared in the block containing the reference. If the referenced variable hasn’t been defined in the block, the compiler attempts to access the variable declared in the next outer block, until a valid access results.