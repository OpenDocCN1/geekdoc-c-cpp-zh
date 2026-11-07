```
```cpp
cout << fixed << showpoint << setprecision(2);

cout << "Enter five test scores: ";

for (index = 0; index < 5; index++)
{
    cin >> test[index];
    sum = sum + test[index];
}

cout << endl;

average = sum / 5.0;

cout << "The average test score = " << average << endl;

for (index = 0; index < 5; index++)
    if (test[index] < average)
        cout << test[index]
             << " is less than the average test score." << endl;
return 0;
}
```
```

**Sample Run:** In this sample run, the user input is shaded.

```
Enter five test scores: 85 62 94 56 71
```

```
The average test score = 73.60
62 is less than the average test score.
56 is less than the average test score.
71 is less than the average test score.
```

# Array Index Out of Bounds

Consider the following declaration:

```
double num[10];
int i;
```

The component num[i] is valid, that is, i is a valid index if i = 0, 1, 2, 3, 4, 5, 6, 7, 8, or 9.

The index—say, index—of an array is in **bounds** if index is between 0 and ARRAY_SIZE − 1, that is, 0 <= index <= ARRAY_SIZE − 1. If index is negative or index is greater than ARRAY_SIZE − 1, then we say that the index is **out of bounds**.

Unfortunately, C++ does not check whether the index value is within range—that is, between 0 and ARRAY_SIZE − 1. If the index goes out of bounds and the program tries to access the component specified by the index, then whatever memory location is indicated by the index that location is accessed. This situation can result in altering or accessing the data of a memory location that you never intended to modify or access, or in trying to access protected memory that causes the program to instantly halt. Consequently, several strange things can happen if the index goes out of bounds during execution. It is solely the programmer’s responsibility to make sure that the index is within bounds.