```
c. ```cpp
for (i = 1; i <= 1; i--)
    cout << "*";
cout << endl;
```
```

```
d. ```cpp
for (i = 12; i >= 9; i--)
    cout << "*";
cout << endl;
```
```

```
e. ```cpp
for (i = 0; i <= 5; i++)
    cout << "*";
cout << endl;
```
```

```
f. ```cpp
for (i = 1; i <= 5; i++)
{
    cout << "*";
    i = i + 1;
}
cout << endl;
```
```

24. Write a `for` statement to add all the multiples of 3 between 1 and 100. (4)

25. What is the output of the following code? Is there a relationship between the variables x and y? If yes, state the relationship? What is the output? (4)

```
```cpp
int x = 19683;
int i;
int y = 0;

for (i = x; i >= 1; i = i / 3)
    y++;
cout << "x = " << x << ", y = " << y << endl;
```
```

26. What is the output of the following code? (4)

```
```cpp
for (int i = 1; i <= 10000; i = 5 * i)
    cout << i << " ";
cout << endl;
```
```

27. What is the output of the following C++ program segment? Assume all variables are properly declared. (4)

```
```cpp
for (j = 0; j < 8; j++)
{
    cout << j * 25 << " - ";

    if (j != 7)
        cout << (j + 1) * 25 - 1 << endl;
    else
        cout << (j + 1) * 25 << endl;
}
```
```

28. Suppose that the input is 3 5 7 −6 10. What is the output of the following code? (4)

```
```cpp
int temp = 0;
int num;
int count;
```
```