```
7. cin >> i1 >> c1 >> i2
    >> c2 >> i3 >> c3;
```

Input: 1A 2B 3C

```
8. cin >> i1 >> i2 >> i3;
```

Input: 012 345 678

```
9. cin >> dec >> i1 >> i2 >> i3;
```

Input: 012 345 678

```
10. cin >> oct >> i1 >> i2 >> i3;
```

Input: 012 345 678

```
11. cin >> hex >> i1 >> i2 >> i3;
```

Input: 12 3A BC

For Exercises 12–20, assume that alpha and beta are real variables with values 2567.392 and 0.004, respectively, and that num1 and num2 are integer variables with values 12 and 436, respectively. Show precisely the output that each of the sets of statements produces, or explain why an error occurs.

```
12. cout << num2 << num2 + 1 << num2 + 2;
```

```
13. cout << num2 << setw(4) << num2 + 1 << num2 + 2;
```

```
14. cout << num1 << num1 + 1 << num1 + 2;
```

```
15. cout << oct << num1 << num1 + 1 << num1 + 2;
```

```
16. cout << showbase << oct << num1 << num1 + 1 << num1 + 2;
```

```
17. cout << hex << num1 << num1 + 1 << num1 + 2;
```

```
18. cout << showbase << hex << num1 << num1 + 1 << num1 + 2;
```

```
19. cout << fixed << showpoint << right
    << setw(9) << setprecision(3) << alpha << endl
    << setw(10) << setprecision(5) << beta << endl
    << setw(7) << setprecision(4) << beta << endl;
```

```
20. cout << scientific << showpoint << left
    << setprecision(1) << setw(10) << alpha << endl
    << setw(5) << beta << endl
    << "Tolerance:"
    << setw(12) << setprecision(3) << beta << endl;
```

For Exercises 21 and 22, assume that i and j are integer variables with values 15 and 8, respectively; that ch is a character variable whose value is 'c'; and that x and y are real variables with values 2559.50 and 8.015, respectively. Show precisely the output produced, or explain why an error occurs.

```
21. cout << setw(j) << setprecision(2)
    << fixed << showpoint << right
```