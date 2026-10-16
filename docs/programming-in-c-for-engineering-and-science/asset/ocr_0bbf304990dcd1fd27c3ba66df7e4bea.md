```
20. for (int i = 0; i < 5; i++)
       if (i % 2 == 0)
           number[i] = 2 * i;
       else
           number[i] = 2 * i + 1;
```

```
21. for (int i = 1; i < 5; i++)
       number[i] = 2 * number[i - 1];
```

```
22. for (int i = 3; i >= 0; i--)
       number[i] = 2 * number[i + 1];
```

# Section 12.6

Questions 1–15 assume that the following statements have been executed:

```
vector<int> a, b(5), c(5, 1), d(5);
d.push_back(77);
d.push_back(88);
```

+   1. The type of values stored in a is ____________.

+   2. The capacity of a is ____________ and its size is ____________.

+   3. The capacity of b is ____________ and its size is ____________.

+   4. The capacity of c is ____________ and its size is ____________.

+   5. The capacity of d is ____________ and its size is ____________.

+   6. What output is produced by
+   
+   ```cpp
+   cout << c.front() << ' ' << c.back() << endl;
+   ```

+   7. What output is produced by
+   
+   ```cpp
+   cout << d.front() << ' ' << d.back() << endl;
+   ```

+   8. (True or false) a.empty().

+   9. (True or false) c < d.

+   10. (True or false) c[1] == 1.

+   11. What output is produced by
+   
+   ```cpp
+   for (int i = 0; i < c.size(); i++)
+       cout << c[i] << ' ';
+   ```