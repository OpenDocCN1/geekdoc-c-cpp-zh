# LESSON 3 Storing Information: Variables and Constants

Operators.” For now, you need to be aware that the equal sign in programming is not the same as the equal sign in algebra. If you write

```
x = 12
```

in an algebraic statement, you are stating a fact: “x equals 12.” In C, however, it means something quite different. In C it means “Assign the value 12 to the variable named x.”

You can also initialize a variable when it’s declared. To do so, follow the variable name in the declaration statement with an equal sign and the initialized value:

```
int count = 0;
double percent = 0.01, taxrate = 28.5;
```

The first statement declares a variable called count as an integer and initializes it to 0. The second statement declares two variables as doubles and initializes them. The first, percent, is initialized to 0.01. The second, taxrate, is initialized to 28.5.

Be careful not to initialize a variable with a value outside the allowed range. Here are two examples of out-of-range initializations:

```
short weight = 100000;
unsigned int value = -2500;
```

The C compiler might not catch such errors. Your program might compile and link, you might get unexpected results when the program runs.

| DO | DON'T |
|---|---|
| DO understand the number of bytes that variable types take for your computer. | DON'T use a variable that hasn't been initialized. Results can be unpredictable. |
| DO use typedef to make your programs more readable. | DON'T use a float or double variable if you're storing only integers. Although they work, using them is inefficient. |
| DO initialize variables when you declare them whenever possible. | DON'T try to put numbers that are too big or too small into a variable if its type won't hold them. |
| | DON'T put negative numbers into variables with an unsigned type. |