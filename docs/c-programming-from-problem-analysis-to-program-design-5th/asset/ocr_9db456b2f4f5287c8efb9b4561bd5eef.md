The program in Example 10-3 illustrates how to use the selection sort algorithm in a program.

# EXAMPLE 10-3

```
//Selection sort

#include <iostream>

using namespace std;

void selectionSort(int list[], int length);

int main()
{
    int list[] = {2, 56, 34, 25, 73, 46, 89, 10, 5, 16}; //Line 1
    int i; //Line 2

    selectionSort(list, 10); //Line 3

    cout << "After sorting, the list elements are:"
         << endl; //Line 4
    for (i = 0; i < 10; i++) //Line 5
        cout << list[i] << " "; //Line 6

    cout << endl; //Line 7

    return 0; //Line 8
}

//place the definition of the function selectionSort given
//previously here.
```

# Sample Run:

```
After sorting, the list elements are:
2 5 10 16 25 34 46 56 73 89
```

This program works the same way as the program in Example 10-1. Here, we use the selection sort algorithm to sort the list.

For a list of length *n*, selection sort makes exactly $\frac{n(n-1)}{2}$ key comparisons and $3(n-1)$ item assignments. Therefore, if $n = 1000$, then to sort the list, selection sort makes about 500,000 key comparisons and about 3000 item assignments. The next section presents the insertion sort algorithm that reduces the number of comparisons.

# Insertion Sort

As noted in the previous section, for a list of length 1000, both bubble sort and selection sort make approximately 500,000 key comparisons, which is quite high. This section