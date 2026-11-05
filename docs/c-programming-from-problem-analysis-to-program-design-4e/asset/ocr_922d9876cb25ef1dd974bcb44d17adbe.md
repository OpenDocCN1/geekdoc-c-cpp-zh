# 11. How many components are allocated by the following statement?

```
double [ ] values = new double [3];
```

+   - a. 32
+   - b. 3
+   - c. 2
+   - d. 4
+   - e. none of the above

# 12. What output is produced by the following code?

```
int i;
int [ ] anArray = new int [5];
for (i = 0; i < anArray.Length; i++)
anArray [i] = 2 * i;
for (i = 0; i < anArray.Length; i++)
Console.Write(anArray [i] + " ");
```

+   - a. 2 2 2 2 2
+   - b. 2 4 6 8 10
+   - c. 0 2 4 6 8 10
+   - d. 0 2 4 6 8
+   - e. none of the above

# 13. If you declare an array as int [ ] anArray = new int[5];
you can double the value stored in anArray [2] with the statement:

```
int [ ] anArray = new int[5];
```

+   - a. anArray [2] = anArray [5] * 2;
+   - b. anArray = anArray * 2;
+   - c. anArray [2] *= anArray [2] * 2;
+   - d. anArray [2] *= 2;
+   - e. none of the above

# 14. With the following declaration:

```
int [ ] points = {550, 700, 900, 800, 100};
```

The statement points [3] = points [3] +10; will

+   - a. replace the 800 amount with 810
+   - b. replace the 550 amount with 560
+   - c. replace the 900 amount with 910
+   - d. result in an error
+   - e. none of the above