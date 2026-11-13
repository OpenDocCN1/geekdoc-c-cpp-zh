
```cpp
quicksort(low, pi - 1);
quicksort(pi + 1, high);
}
```

### merge sort

```cpp
void mergesort(int l, int r)
{
    if (l < r)
    {
        int m = l + (r - l) / 2;
        // Sort first and second halves
        mergesort(l, m);
        mergesort(m + 1, r);
        merge(l, m, r);
    }
}

void merge(int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 = r - m;
    int L[n1], R[n2];
    for (i = 0; i < n1; i++)
        L[i] = a[l + i];
    for (j = 0; j < n2; j++)
        R[j] = a[m + 1 + j];
    i = 0;
    j = 0;
    k = l; // index for merge array
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            a[k] = L[i];
            i++;
        }
        else
        {
            a[k] = R[j];
            j++;
        }
        k++;
    }
    // copy the rest elements of left array
    while (i < n1)
    {
        a[k] = L[i];
        i++;
        k++;
    }
    // copy the remaining elements of right array
    while (j < n2)
    {
        a[k] = R[j];
        j++;
        k++;
    }
}
```

### bubble sort

```cpp
void bubble(int n)
{
    int i, j;
    for (i = 0; i < n; ++i)
    {
        for (j = 0; j < n - 1 - i; ++j)
        {
            if (a[j] > a[j + 1])
            {
                a[j] = a[j] + a[j + 1];
                a[j + 1] = a[j] - a[j + 1];
                a[j] = a[j] - a[j + 1];
            }
        }
    }
}
```

### insertion sort

```cpp
void insertion(int n)
{
    int k, t, j;
    for (int k = 1; k < n; k++)
    {
        t = a[k];
        j = k - 1;
        while (j >= 0 && t < a[j])
        {
            a[j + 1] = a[j];
            j = j - 1;
        }
        a[j + 1] = t;
    }
}
```

### driver program

```cpp
int main()
{
    int timetaken[5][6], i, j;
    clock_t start, finish;
    double duration;

    // selection sort
    // assign 10000 to n
    n = 10000;
    input(n);
    start = clock(); // time in milliseconds
    selection(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[0][0] = duration;
    delete a;

    // assign 20000 to n
    n = 20000;
    input(n);
    start = clock(); // time in milliseconds
    selection(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[1][0] = duration;
    delete a;

    // assign 30000 to n
    n = 30000;
    input(n);
    start = clock(); // time in milliseconds
    selection(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[2][0] = duration;
    delete a;

    // assign 40000 to n
    n = 40000;
    input(n);
    start = clock(); // time in milliseconds
    selection(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[3][0] = duration;
    delete a;

    // assign 50000 to n
    n = 50000;
    input(n);
    start = clock(); // time in milliseconds
    selection(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[4][0] = duration;
    delete a;

    // heap sort
    // assign 10000 to n
    n = 10000;
    input(n);
    start = clock(); // time in milliseconds
    heapsort(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[0][1] = duration;
    delete a;

    // assign 20000 to n
    n = 20000;
    input(n);
    start = clock(); // time in milliseconds
    heapsort(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[1][1] = duration;
    delete a;

    // assign 30000 to n
    n = 30000;
    input(n);
    start = clock(); // time in milliseconds
    heapsort(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[2][1] = duration;
    delete a;

    // assign 40000 to n
    n = 40000;
    input(n);
    start = clock(); // time in milliseconds
    heapsort(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[3][1] = duration;
    delete a;

    // assign 50000 to n
    n = 50000;
    input(n);
    start = clock(); // time in milliseconds
    heapsort(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[4][1] = duration;
    delete a;

    // quick sort
    // assign 10000 to n
    n = 10000;
    input(n);
    start = clock(); // time in milliseconds
    quicksort(0, n - 1);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[0][2] = duration;
    delete a;

    // assign 20000 to n
    n = 20000;
    input(n);
    start = clock(); // time in milliseconds
    quicksort(0, n - 1);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[1][2] = duration;
    delete a;

    // assign 30000 to n
    n = 30000;
    input(n);
    start = clock(); // time in milliseconds
    quicksort(0, n - 1);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[2][2] = duration;
    delete a;

    // assign 40000 to n
    n = 40000;
    input(n);
    start = clock(); // time in milliseconds
    quicksort(0, n - 1);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[3][2] = duration;
    delete a;

    // assign 50000 to n
    n = 50000;
    input(n);
    start = clock(); // time in milliseconds
    quicksort(0, n - 1);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[4][2] = duration;
    delete a;

    // merge sort
    // assign 10000 to n
    n = 10000;
    input(n);
    start = clock(); // time in milliseconds
    mergesort(0, n - 1);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[0][3] = duration;
    delete a;

    // assign 20000 to n
    n = 20000;
    input(n);
    start = clock(); // time in milliseconds
    mergesort(0, n - 1);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[1][3] = duration;
    delete a;

    // assign 30000 to n
    n = 30000;
    input(n);
    start = clock(); // time in milliseconds
    mergesort(0, n - 1);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[2][3] = duration;
    delete a;

    // assign 40000 to n
    n = 40000;
    input(n);
    start = clock(); // time in milliseconds
    mergesort(0, n - 1);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[3][3] = duration;
    delete a;

    // assign 50000 to n
    n = 50000;
    input(n);
    start = clock(); // time in milliseconds
    mergesort(0, n - 1);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[4][3] = duration;
    delete a;

    // bubble sort
    // assign 10000 to n
    n = 10000;
    input(n);
    start = clock(); // time in milliseconds
    bubble(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[0][4] = duration;
    delete a;

    // assign 20000 to n
    n = 20000;
    input(n);
    start = clock(); // time in milliseconds
    bubble(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[1][4] = duration;
    delete a;

    // assign 30000 to n
    n = 30000;
    input(n);
    start = clock(); // time in milliseconds
    bubble(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[2][4] = duration;
    delete a;

    // assign 40000 to n
    n = 40000;
    input(n);
    start = clock(); // time in milliseconds
    bubble(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[3][4] = duration;
    delete a;

    // assign 50000 to n
    n = 50000;
    input(n);
    start = clock(); // time in milliseconds
    bubble(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[4][4] = duration;
    delete a;

    // insertion sort
    // assign 10000 to n
    n = 10000;
    input(n);
    start = clock(); // time in milliseconds
    insertion(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[0][5] = duration;
    delete a;

    // assign 20000 to n
    n = 20000;
    input(n);
    start = clock(); // time in milliseconds
    insertion(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[1][5] = duration;
    delete a;

    // assign 30000 to n
    n = 30000;
    input(n);
    start = clock(); // time in milliseconds
    insertion(n);
    finish = clock(); // time in milliseconds
    duration = (double)(finish - start); // time in secs.
    timetaken[2][5] = duration;
    delete a;

    // assign 40000 to n
    n = 40000;
    input(n);
    start = clock(); // time in milliseconds
    insertion(n);
```
