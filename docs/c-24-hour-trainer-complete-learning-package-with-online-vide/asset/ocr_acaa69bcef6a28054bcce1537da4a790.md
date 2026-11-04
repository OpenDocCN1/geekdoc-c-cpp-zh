> NOTE The notation 7.9e28 means 7.9 × 10²⁸.

Note that rounding errors can still occur when you combine decimal values. For example, if you add 1e28 plus 1e-28, the result would have more than the 28 or 29 significant digits that a decimal can provide so it rounds off to 1e28.

The moral of the story is that you should always use the decimal data type for values where you need great accuracy and the values won't get truly enormous. In particular, you should always use decimal for currency values. Unless you're Bill Gates's much richer uncle, you'll never get close to the largest value a decimal can represent, and the extra precision can prevent rounding errors during some fairly complex calculations.

> NOTE Another interesting feature of the decimal type is that, because of the way it stores its significant digits, it remembers zeros on the right. For example, if you add the values 1.35 and 1.65 as floats, you get the value 3. In contrast, if you add the same values as decimals, you get 3.00. The decimal result remembers that you were working with two digits to the right of the decimal point so it stores the result that way, too.

# DECLARING VARIABLES

To declare a variable in C# code, give the data type that you want to use followed by the name that you want to give the variable. For example, the following code creates a variable named numMistakes. The variable's data type is int so it can hold an integer between −2,147,483,648 and 2,147,483,647 (which should be enough for most projects that don't involve the government):

```
int numMistakes;
```

You can use the equals symbol to assign a value to a variable. For example, the following code sets numMistakes to 1337:

```
numMistakes = 1337;
```

As an added convenience, you can declare a variable and give it a value at the same time, as in:

```
int numMistakes = 1337;
```

You can declare several variables of the same type all at once by separating them with commas. You can even initialize them if you like. The following code declares three float variables named x, y, and z and gives them initial values of 1, 2, and −40, respectively:

```
float x = 1, y = 2, z = -40;
```