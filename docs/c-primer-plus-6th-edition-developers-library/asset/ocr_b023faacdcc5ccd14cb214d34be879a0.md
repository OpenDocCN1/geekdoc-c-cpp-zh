# Example:

```
for (n = 0; n < 10 ; n++)
    printf(" %d %d\n", n, 2 * n + 1);
```

# More Assignment Operators: +=, -=, *=, /=, %=

C has several assignment operators. The most basic one, of course, is =, which simply assigns the value of the expression at its right to the variable at its left. The other assignment operators update variables. Each is used with a variable name to its left and an expression to its right. The variable is assigned a new value equal to its old value adjusted by the value of the expression at the right. The exact adjustment depends on the operator. For example,

```
scores += 20 is the same as scores = scores + 20.
```

```
dimes -= 2 is the same as dimes = dimes - 2.
```

```
bunnies *= 2 is the same as bunnies = bunnies * 2.
```

```
time /= 2.73 is the same as time = time / 2.73.
```

```
reduce %= 3 is the same as reduce = reduce % 3.
```

The preceding list uses simple numbers on the right, but these operators also work with more elaborate expressions, such as the following:

```
x *= 3 * y + 12 is the same as x = x * (3 * y + 12).
```

The assignment operators we've just discussed have the same low priority that = does—that is, less than that of + or *. This low priority is reflected in the last example in which 12 is added to 3 * y before the result is multiplied by x.

You are not required to use these forms. They are, however, more compact, and they may produce more efficient machine code than the longer form. The combination assignment operators are particularly useful when you are trying to squeeze something complex into a for loop specification.

# The Comma Operator

The comma operator extends the flexibility of the for loop by enabling you to include more than one initialization or update expression in a single for loop specification. For example, Listing 6.13 shows a program that prints first-class postage rates. (At the time of this writing, the rate is 46 cents for the first ounce and 20 cents for each additional ounce. You can check the Internet for the current rates.)