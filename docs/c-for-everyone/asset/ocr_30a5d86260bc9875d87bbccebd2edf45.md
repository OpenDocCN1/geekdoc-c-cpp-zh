```
```cpp
50       if (min_pos != next)
51       {
52          swap(a[min_pos], a[next]);
53       }
54    }
55 }
56
57 /*
58    Prints all elements in an array.
59    @param a the array to print
60    @param size the number of elements in a
61 */
62 void print(int a[], int size)
63 {
64    for (int i = 0; i < size; i++)
65    {
66       cout << a[i] << " ";
67    }
68    cout << endl;
69 }
70
71 int main()
72 {
73    srand(time(0));
74    const int SIZE = 20;
75    int values[SIZE];
76    for (int i = 0; i < SIZE; i++)
77    {
78       values[i] = rand() % 100;
79    }
80    print(values, SIZE);
81    selection_sort(values, SIZE);
82    print(values, SIZE);
83    return 0;
84 }
```
```

# Program Run

```
```text
60 47 70 39 6 12 96 93 83 53 36 29 50 97 94 95 38 17 8 26
6 8 12 17 26 29 36 38 39 47 50 53 60 70 83 93 94 95 96 97
```
```

![](bbox=[0.075, 0.66, 0.2, 0.77])

+   1. What steps does the selection sort algorithm go through to sort the array 6 5 4 3 2 1?
+   2. How can you change the selection sort algorithm so that it sorts the elements in descending order (that is, with the largest element at the beginning of the array)?
+   3. Suppose we modified the selection sort algorithm to start at the end of the array, working toward the beginning. In each step, the current position is swapped with the minimum. What is the result of this modification?
+   4. Why do we need the temp variable in the swap function? What would happen if you simply assigned a[i] to a[j] and a[j] to a[i]?

**Practice It** Now you can try these exercises at the end of the chapter: R12.1, P12.1, P12.2.