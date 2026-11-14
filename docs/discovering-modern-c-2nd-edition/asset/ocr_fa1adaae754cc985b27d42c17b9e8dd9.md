As the name suggests, a `while`-loop is repeated as long as the given condition holds. Let us implement as an example the Collatz series that is defined by

# Algorithm 1–1: Collatz series

```
Input: x0
1 while xi != 1 do
   xi = { 3xi-1 + 1 if xi-1 is odd
          xi-1/2   if xi-1 is even
2
```

If we do not worry about overflow, this is easily implemented with a `while`-loop:

Click here to view code image

```
int x= 19;
while (x != 1) {
cout << x << '\n';
if (x % 2 == 1) // odd
x= 3 * x + 1;
else // even
x= x / 2;
}
```

Like the `if`-statement, the loop can be written without braces in case of a single statement.

C++ also offers a `do`-`while`-loop. There the condition for continuation is tested at the end:

Click here to view code image

```
double eps = 0.001;
do {
cout << "eps= " << eps << '\n';
eps/= 2.0;
} while (eps > 0.0001);
```

The loop is performed at least once regardless of the condition.

# 1.4.4.2 for-Loop