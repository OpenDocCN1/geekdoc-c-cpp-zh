```
```cpp
for(int pass = 0; pass < n-1; pass++)
{
    min_index = pass;
    for(i = pass + 1; i < n; i++)
    {
        if(a[i] < a[min_index])
            min_index = i;
    } // innermost for loop
    if(pass != min_index)
    {
        temp = a[pass];
        a[pass] = a[min_index];
        a[min_index] = temp;
    }
} // outermost for loop

void main()
{
    array obj;
    int n;
    cout << "Enter no of elements << = " << size << "\n";
    cin >> n;
    cout << "\nEnter " << n << " elements\n";
    obj.enter(n);
    // echo the data
    cout << "\nGiven array is \n\n";
    obj.display(n);
    obj.selection_sort(n);
    cout << "\n\n After applying selection sort array
                 is :\n";
    obj.display(n);
}
```
```

**OUTPUT :**

Enter no of elements << = 20  
6  
Enter 6 elements  
10 17 23 5 3 89  
Given array is  
10 17 23 5 3 89  
After applying selection sort array is :  
3 5 10 17 23 89