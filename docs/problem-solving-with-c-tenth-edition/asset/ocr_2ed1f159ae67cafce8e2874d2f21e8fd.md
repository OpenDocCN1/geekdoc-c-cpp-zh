# 3. Identify any errors in the following array declarations:

+   a. `int x[4] = { 8, 7, 6, 4, 3 };`
+   b. `int x[ ] = { 8, 7, 6, 4 };`
+   c. `const int SIZE = 4;`
+   d. `int x[SIZE];`

# 4. What is the output of the following code?

```
char symbol[3] = {'a', 'b', 'c'};

for (int index = 0; index < 3; index++)
    cout << symbol[index];
```

# 5. What is the output of the following code?

```
double a[3] = {1.1, 2.2, 3.3};
cout << a[0] << " " << a[1] << " " << a[2] << endl;
a[1] = a[2];
cout << a[0] << " " << a[1] << " " << a[2] << endl;
```

# 6. What is the output of the following code?

```
int i, temp[10];

for (i = 0; i < 10; i++)
    temp[i] = 2 * i;

for (i = 0; i < 10; i++)
    cout << temp[i] << " ";
cout << endl;

for (i = 0; i < 10; i = i + 2)
    cout << temp[i] << " ";
```

# 7. What is wrong with the following piece of code?

```
int sampleArray[10];

for (int index = 1; index <= 10; index++)
    sampleArray[index] = 3 * index;
```

# 8. Suppose we expect the elements of the array a to be ordered so that a[0] ≤ a[1] ≤ a[2] ≤ ...

However, to be safe we want our program to test the array and issue a warning in case it turns out that some elements are out of order. The following code is supposed to output such a warning, but it contains a bug. What is it?

```
double a[10];
<Some code to fill the array a goes here.>
```