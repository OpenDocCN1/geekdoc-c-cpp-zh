# sort() method

The method `sort()` is used to sort the elements in the collection in ascending order by default. The program demonstrates sorting of linked list containing integer values.

```
```cpp
#include<list.h>
void main()
{
    list<int> l1;
    int i;
    for(i=10;i>=1;i--)
    {
        l1.push_back(i);
    }
    //sort the elements of the list
    l1.sort();
    cout<<"Sorted list"<<endl;
    list<int> :: iterator temp;
    for(temp = l1.begin();temp != l1.end() ; temp++)
    {
        cout<<*temp<<" ";
    }
}
```
```

# Output

```
```text
Sorted list
1 2 3 4 5 6 7 8 9 10
```
```

The statement

```
```cpp
l1.sort();
```
```

invokes a `sort()` method which arranges the linked list l1 in ascending order.

# Defining custom logic for comparison

It is possible to define a custom comparison logic to `sort()` method. An overloaded version of `sort()` is available in STL, which accepts a user-defined function as an argument. This user-defined function can define the logic on how should the `sort()` method perform comparison of any two elements in the linked list.

We have learnt sorting of arrays in Chapter 6 Section 6.2.5, recall that the process of sorting compared two elements at any point in time. Hence, the user-defined function we would create to customize the sorting process must define the logic on how any two elements of the list are to be compared. If the user-defined function returns 1 (true), it means that two elements in the list are in correct order; whereas, if the user-defined function returns 0 (false), it means that the two elements in the list are in the incorrect order and their positions need to be interchanged.