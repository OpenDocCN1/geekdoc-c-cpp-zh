Here is a sample run of the program in Listing 6.9:

```
```
Enter two integers: 25 28
The larger of 25 and 28 is 28
```
```

The key part of the program is this statement:

```
```cpp
int c = a > b ? a : b;
```
```

It produces the same result as the following statements:

```
```cpp
int c;
if (a > b)
    c = a;
else
    c = b;
```
```

Compared to the if else sequence, the conditional operator is more concise but, at first glance, less obvious. One difference between the two approaches is that the conditional operator produces an expression and hence a single value that can be assigned or be incorporated into a larger expression, as the program in Listing 6.9 does when it assigns the value of the conditional expression to the variable c. The conditional operator's concise form, unusual syntax, and overall weird appearance make it a great favorite among programmers who appreciate those qualities. One favorite trick for the reprehensible goal of concealing the purpose of code is to nest conditional expressions within one another, as the following mild example shows:

```
```cpp
const char x[2] [20] = {"Jason ", "at your service\n"};
const char * y = "Quillstone ";

for (int i = 0; i < 3; i++)
    cout << ((i < 2)? i ? x[i] : y : x[1]);
```
```

This is merely an obscure (but, by no means maximally obscure) way to print the three strings in the following order:

```
```
Jason Quillstone at your service
```
```

In terms of readability, the conditional operator is best suited for simple relationships and simple expression values:

```
```cpp
x = (x > y) ? x : y;
```
```

If the code becomes more involved, it can probably be expressed more clearly as an if else statement.

# ## The switch Statement

Suppose you create a screen menu that asks the user to select one of five choices—for example, Cheap, Moderate, Expensive, Extravagant, and Excessive. You can extend an if else if else sequence to handle five alternatives, but the C++ switch statement more