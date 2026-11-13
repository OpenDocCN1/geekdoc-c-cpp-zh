From Fig. 12.19, we can see that we have reached a leaf and can stop now.
Let us see how this can be implemented using C++ in Program Code 12.2.

```
PROGRAM CODE 12.2
// ReheapDown operation is required when deleting an
// element from top location
void Heap :: ReHeapDown(int i)
{
    int temp;
    while(2 * i < n)
    {
        j = 2 * i + 1;
        // j index shows the left child of the node
        if(j + 1 < n && a[j + 1] > a[j])
        // finding max from left and right child
        j = j + 1;
        if(a[i] > a[j]) break;
        // if root > children then break
        else
        {
            // swap a[i] with a[j]
            temp = a[i];
            a[i] = a[j];
            a[j] = temp;
            i = j;
        }
    } // end of while
}
// Following is the code for function for deleting
// maximum value from heap.
void Heap :: Delete_MaxVal()
{
    int temp;
    // swap 0th element with last value of an array
    temp = a[0];
    a[0] = a[n - 1];
    a[n - 1] = temp;
    // reheapdown operation is called to delete max
    // value from first location
    ReHeapDown(0);
}
```