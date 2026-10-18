```
19. `bool search(const int a[ ], int numberUsed, int target, int& where)`
{
    int index = 0;
    bool found = false;
    while ((!found) && (index < numberUsed))
        if (target == a[index])
            found = true;
        else
            index++;
    //If target was found, then
    //found == true and a[index] == target.
    if (found)
        where = index;
    return found;
}
```

+   20.
+   ```
+   0 1 2 3
+   0 1 2 3
+   0 1 2 3
+   0 1 2 3
+   ```

```
21. `int a[4][5];`
`int index1, index2;`
`for (index1 = 0; index1 < 4; index1++)`
`    for (index2 = 0; index2 < 5; index2++)`
`        cin > a[index1][index2];`
```

```
22. `void echo(const int a[][5], int sizeOfA)`
//Outputs the values in the array a on sizeOfA lines
//with 5 numbers per line.
{
    for (int index1 = 0; index1 < sizeOfA; index1++)
    {
        for (int index2 = 0; index2 < 5; index2++)
            cout << a[index1][index2] << " ";
        cout << endl;
    }
}
```

# PRACTICE PROGRAMS

Practice Programs can generally be solved with a short program that directly applies the programming principles presented in this chapter.

+   1. Write a function called `findMax` which takes as input an array of *doubles* which are greater than zero and an integer which specifies how many elements there are in the array. The function should return the largest value in the array. Write a driver program to test your function with arrays of