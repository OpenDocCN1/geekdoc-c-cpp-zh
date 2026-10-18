# DISPLAY 7.12  Sorting an Array (part 2 of 2)

```
```cpp
{//Place the correct value in a[index]:
    indexOfNextSmallest =
            indexOfSmallest(a, index, numberUsed);
    swapValues(a[index], a[indexOfNextSmallest]);
    //a[0] <= a[1] <=...<= a[index] are the smallest of the original array
    //elements. The rest of the elements are in the remaining positions.
}
```
```

```
```cpp
void swapValues(int& v1, int& v2)
{
    int temp;
    temp = v1;
    v1 = v2;
    v2 = temp;
}
```
```

```
```cpp
int indexOfSmallest(const int a[], int startIndex, int numberUsed)
{
    int min = a[startIndex];
    int indexOfMin = startIndex;
    for (int index = startIndex + 1; index < numberUsed; index++)
        if (a[index] < min)
        {
            min = a[index];
            indexOfMin = index;
            //min is the smallest of a[startIndex] through a[index]
        }

    return indexOfMin;
}
```
```

# Sample Dialogue

```
```text
This program sorts numbers from lowest to highest.
Enter up to 10 nonnegative whole numbers.
Mark the end of the list with a negative number.
80 30 50 70 60 90 20 30 40 -1
In sorted order the numbers are:
20 30 30 40 50 60 70 80 90
```
```