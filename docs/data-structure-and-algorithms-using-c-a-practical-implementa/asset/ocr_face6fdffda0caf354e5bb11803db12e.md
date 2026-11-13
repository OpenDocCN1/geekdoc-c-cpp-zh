```
```cpp
k++;
}
//copy the rest elements of left array
while (i < n1)
{
    a[k] = L[i];
    i++;
    k++;
}
//copy the remaining elements of right array
while (j < n2)
{
    a[k] = R[j];
    j++;
    k++;
}
}
```
```

```
```cpp
//bubble sort
void bubble(int n)
{
    int i, j;
    for (i = 0; i < n; ++i)
    {
        for (j = 0; j < n-1-i; ++j)
        {
            if (a[j] > a[j+1])
            {
                a[j] = a[j]+a[j+1];
                a[j+1] = a[j]-a[j + 1];
                a[j] = a[j]-a[j + 1];
            }
        }
    }
}
```
```

```
```cpp
//insertion sort
void insertion(int n)
{
    int k,t,j;
    for(int k=1; k<n; k++)
    {
        t = a[k];
```
```