```
for(i = 0; i < SIZE; i++)
{
    cout << "Enter name: ";
    getline(cin, name[i]);

    cout << "Enter grade: ";
    cin >> grd[i];
    cin.get();
}
sel_sort(name, grd);
```

```
cout << "\n***** Final Rating *****\n";
for(i = 0; i < SIZE; i++)
    cout << name[i] << " \\t <<" << grd[i] << " \\n";
    return 0;
```

```
void sel_sort(vector<string>& str, double arr[])
{
    int i, j;
    double K;
    string tmp;

    for(i = 0; i < SIZE-1; i++)
    {
        for(j = i+1; j < SIZE; j++)
        {
            if(arr[i] > arr[j])
            {
                // Parallel swapping of grades and names.
                k = arr[i];
                arr[i] = arr[j];
                arr[j] = k;

                tmp = str[j];
                str[j] = str[i];
                str[i] = tmp;
            }
        }
    }
}
```

C.12.7 Write the add_sort() function that inserts a number into a sorted array, so that the array remains sorted. Write a program that reads nine integers, stores them in an array of ten integers, and sorts these elements in ascending order. Then, the program should read the last integer, use the add_sort() to insert it in the array and display the sorted array.

```
#include <iostream>
using std::cout;
using std::cin;
```

```
void sel_sort(int arr[], int size);
void add_sort(int arr[], int size, int num);
```