```
```cpp
cout << endl;
for (j = 0; j < 5; j++)
{
    two[j] = 2 * one[j] - 1;
    two[j + 5] = one[4 - j] + two[j];
}

cout << "Two contains: ";
for (j = 0; j < 10; j++)
    cout << two[j] << " ";
cout << endl;

return 0;
}
```
```

27. What is the output of the following C++ code?

```
```cpp
const double PI = 3.14159;
double cylinderRadii[5] = {3.5, 7.2, 10.5, 9.8, 6.5};
double cylinderHeights[5] = {10.7, 6.5, 12.0, 10.5, 8.0};
double cylinderVolumes[5];

cout << fixed << showpoint << setprecision(2);

for (int i = 0; i < 5; i++)
    cylinderVolumes[i] = 2 * PI * cylinderRadii[i]
                         * cylinderHeights[i];

for (int i = 0; i < 5; i++)
    cout << (i + 1) << " " << cylinderRadii[i] << " "
         << cylinderHeights[i] << " " << cylinderVolumes[i] << endl;
```
```

28. When an array is passed as an actual parameter to a function, what is actually being passed?

29. In C++, as an actual parameter, can an array be passed by value?

30. Sort the following list using the selection sort algorithm as discussed in this chapter. Show the list after each iteration of the outer for loop.

6, 45, 10, 25, 58, 2, 50, 30, 86

31. Sort the following list using the selection sort algorithm as discussed in this chapter. Show the list after each iteration of the outer for loop.

36, 55, 17, 35, 63, 85, 12, 48, 3, 66

32. Given the declaration:

```
```cpp
char string15[16];
```
```

Mark the following statements as valid or invalid. If a statement is invalid, explain why.

+   a. `strcpy(string15, "Hello there");`
+   
+   b. `strlen(string15);`
+   
+   c. `string15 = "Jacksonville";`