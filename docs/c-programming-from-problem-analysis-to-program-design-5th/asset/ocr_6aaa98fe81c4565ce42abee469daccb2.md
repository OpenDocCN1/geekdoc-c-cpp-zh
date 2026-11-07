```
```cpp
b.  number = 1;
    do
    {
        cout << setw(3) << number;
        number++;
    }
    while (number <= 10);
```
```

+   41.  11 18 25
+   
+   43.  −1 0 3 8 15 24
+   
+   45.  12 11 9 7 6 4 2 1

# Chapter 6

+   1.  a. false; b. true; c. true; d. true; e. false

+   3.  a. 4    b. 10.8    c. 2.5    d. 10.24    e. 15.625
+       f. 5    g. 2.5    h. 9    i. 28    j. 36

+   5.  (iii)

+   7.  a, b, c, e, f, and g are valid. In d, the function call in the output (cout) statement requires one more argument.

+   9.  a.  4; `int`
+       b.  2; `double`
+       c.  4; `char`
+       d.  The function test requires four actual parameters. The order of the parameters is: `int`, `char`, `double`, `int`.
+       e.  `cout << test(5, '2', 7.3, 5) << endl;`
+       f.  `cout << two(17.5, 18.3) << endl;`
+       g.  `cout << static_cast<char>(static_cast<int>(three(4, 3, 'A', 17.6)) + 1) << endl;`

```
```cpp
11.  bool isUppercaseLetter(char ch)
     {
         if (isupper(ch))
             return true;
         else
             return false;
     }
```
```

+   13.  a.  i. 125    ii. 432
+         b.  The function computes x³, in which x is the argument of the function.

+   15.  1 4 9 16 25 36 49 64 81 100