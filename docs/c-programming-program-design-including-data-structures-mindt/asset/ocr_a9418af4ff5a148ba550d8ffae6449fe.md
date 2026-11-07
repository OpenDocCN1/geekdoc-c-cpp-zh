```
c.  `cin >> x;`
    `cin.get(ch);`
    `cin >> y >> z;`

d.  `cin >> x >> ch >> y >> z;`
    `cin.get(ch);`

e.  `cin >> x >> y >> z;`
```

3. Suppose `int1` and `int2` are int variables and `dec1` and `dec2` are double variables. Assume the following input data: (2)

`56.50 67 48 62.72`

What value (if any) is assigned to `int1`, `int2`, `dec1`, and `dec2` after each of the following statements executes? (Use the same input for each statement.)

+   a. `cin >> dec1 >> int1 >> int2 >> dec2;`
+   
+   b. `cin >> int1 >> dec1 >> dec2 >> int1;`
+   
+   c. `cin >> dec1 >> dec2 >> int1 >> int2;`
+   
+   d. `cin >> int1 >> dec1 >> int2 >> dec2;`
+   
+   e. `cin >> int1 >> int2 >> dec1 >> dec2;`

4. Suppose `x` and `y` are int variables and `symbol` is a char variable. Assume the following input data:

```
`38 26 * 67 33`
`24 $ 55 # 34`
`# & 63 85`
```

What value (if any) is assigned to `x`, `y`, and `symbol` after each of the following statements executes? (Use the same input for each statement.)

(2, 3, 4)

+   a.
+   ```cpp
+   cin >> x >> y;
+   cin.ignore(100, '\n');
+   cin >> symbol;
+   ```
+   
+   b.
+   ```cpp
+   cin >> x;
+   cin.ignore(100, '*');
+   cin >> y;
+   cin.get(symbol);
+   ```
+   
+   c.
+   ```cpp
+   cin >> y;
+   cin.ignore(100, '\n');
+   cin >> x >> symbol;
+   ```
+   
+   d.
+   ```cpp
+   cin.get(symbol);
+   cin.ignore(100, '*');
+   cin >> x;
+   cin.ignore(100, '\n');
+   cin >> y;
+   ```