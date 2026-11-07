+   7. Consider the following statements:

```
```
linkedStackType<int> stack;
long long num;
int temp;
int secretNum = 0;
```
```

Show what is output by the following segment of code, if the input is 837298651020706. (4)

```
```
cin >> num;

num = abs(num);

while (num > 0)
{
    stack.push(num % 100);
    num = num / 100;
}

while (!stack.isEmptyStack())
{
    temp = stack.top();
    stack.pop();
    secretNum = secretNum + temp;
}

cout << "secretNum = " << secretNum << endl;
```
```

+   8. What does the program segment in Exercise 7 do? (4)

+   9. Evaluate the following postfix expressions: (5)

+   a. 12 18 - 30 + 2 * 3 / =
+   b. 28 5 / 3 + 5 4 * - 8 + =
+   c. 13 18 10 17 2 20 + - + / * =
+   d. 7 3 6 2 + - + 2 * 8 + =
+   e. 29 3 / 6 + 12 - 3 4 * + =

+   10. Convert the following infix expressions to postfix notations: (5)

+   a. x + y + z - w / t
+   b. x - (y + z) * w + (t - u) / s
+   c. ((x + y) / z * (u - v)) / t + w
+   d. x / y / z + (u * v * t) / w - s

+   11. Write the equivalent infix expression for the following postfix expressions. (5)

+   a. x y * z + t -
+   b. x y z + * w u / -