# REVIEW EXERCISES

R6.1 Carry out the following tasks with an array:

+   - a. Allocate an array a of ten integers.
+   - b. Put the number 17 as the initial element of the array.
+   - c. Put the number 29 as the last element of the array.
+   - d. Fill the remaining elements with -1.
+   - e. Add 1 to each element of the array.
+   - f. Print all elements of the array, one per line.
+   - g. Print all elements of the array in a single line, separated by commas.

R6.2 Write code that fills an array double values[10] with each set of values below.

+   - a. 1 2 3 4 5 6 7 8 9 10
+   - b. 0 2 4 6 8 10 12 14 16 18 20
+   - c. 1 4 9 16 25 36 49 64 81 100
+   - d. 0 0 0 0 0 0 0 0 0 0
+   - e. 1 4 9 16 9 7 4 9 11
+   - f. 0 1 0 1 0 1 0 1 0 1
+   - g. 0 1 2 3 4 0 1 2 3 4

R6.3 Consider the following array:

```
int a[] = { 1, 2, 3, 4, 5, 4, 3, 2, 1, 0 };
```

What is the value of total after the following loops complete?

+   - a. int total = 0;
+     for (int i = 0; i < 10; i++) { total = total + a[i]; }
+   - b. int total = 0;
+     for (int i = 0; i < 10; i = i + 2) { total = total + a[i]; }
+   - c. int total = 0;
+     for (int i = 1; i < 10; i = i + 2) { total = total + a[i]; }
+   - d. int total = 0;
+     for (int i = 2; i <= 10; i++) { total = total + a[i]; }
+   - e. int total = 0;
+     for (int i = 1; i < 10; i = 2 * i) { total = total + a[i]; }
+   - f. int total = 0;
+     for (int i = 9; i >= 0; i--) { total = total + a[i]; }
+   - g. int total = 0;
+     for (int i = 9; i >= 0; i = i - 2) { total = total + a[i]; }
+   - h. int total = 0;
+     for (int i = 0; i < 10; i++) { total = a[i] - total; }

R6.4 Consider the following array:

```
int a[] = { 1, 2, 3, 4, 5, 4, 3, 2, 1, 0 };
```

What are the contents of the array a after the following loops complete?