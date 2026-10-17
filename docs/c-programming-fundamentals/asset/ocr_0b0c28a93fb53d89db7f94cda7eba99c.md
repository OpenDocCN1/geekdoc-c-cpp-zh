Driver is: 10  
Driver is: 2

# 3.2.4 Searching

Accessing each and every element of an array by index (called *traversing*) is not efficient for large arrays, so we should work with an algorithm to search for the element we are looking for. These search methods are as follows.

# Linear Search

In a linear search, we sequentially search for the element needed by traversing through the array and checking whether the search element matches the array element.

# Algorithm for a Linear Search

+   1. Start.
+   2. Take the size and element input from a user if the array is not given.
+   3. Input the search element from the user.
+   4. Initialize the for loop from i=0 to index size-1.
+   5. Use a nested if loop for the search element == array[i].
+   6. If the result is true, then a match is found; break out of the loop.
+   7. If the result is false, then execute the else part of the code.
+   8. Stop.

# Code: Example of a Linear Search

```
```cpp
#include<iostream>
using namespace std;
int main()
{
        int size,e,flag=0;
        cout<<"\nGive the size of the array "<<endl;
        cin>>size;
        int array[size];
        cout<<"Enter the elements of the array "<<endl;
        for(int i=0;i<size;i++)
        {
                cin>>array[i];
```
```