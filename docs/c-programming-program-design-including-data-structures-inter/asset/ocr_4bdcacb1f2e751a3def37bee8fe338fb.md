21. Consider the following function heading:

```
```cpp
void tryMe(int x[], int size);
```
```

and the declarations:

```
```cpp
int list[100];
int score[50];
double gpas[50];
```
```

Which of the following function calls is valid?

+   a. tryMe(list, 100);
+   b. tryMe(list, 75);
+   c. tryMe(score, 100);
+   d. tryMe(score, 49);
+   e. tryMe(gpas, 50);

22. Suppose that you have the following function definition:

```
```cpp
void sum(int x, int y, int& z)
{
    z = x + y;
}
```
```

Consider the following declarations:

```
```cpp
int list1[10], list2[10], list3[10];
int a, b, c;
```
```

Which of the following function calls is valid?

+   a. sum(a, b, c);
+   b. sum(list1[0], list2[0], a);
+   c. sum(list1, list2, c);
+   d. for (int i = 1; i <= 10; i++)
+          sum(list1[i], list2[i], list3[i]);

23. What is the output of the following C++ code?

```
```cpp
double salary[5] = {25000, 36500, 85000, 62500, 97000};
double raise = 0.03;

cout << fixed << showpoint << setprecision(2);

for (int i = 0; i < 5; i++)
    cout << (i + 1) << " " << salary[i] << " "
         << salary[i] * raise << endl;
```
```

24. A car dealer has 10 salespersons. Each salesperson keeps track of the number
of cars sold each month and reports it to the management at the end of the
month. The management keeps the data in a file and assigns a number, 1 to
10, to each salesperson. The following statement declares an array, cars, of