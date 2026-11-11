```
```cpp
cout << "Sorted Array:" << endl;
for (int i = 0; i <5; i++)
    cout << a[i] << " ";
return 0;
}
```
```

Output:

Sorted Array:

2 3 5 7 9

In the example above, when we pass array name an as an argument, we are telling the function, to sort at the beginning of the array. If we wanted it to start the sort at the third element of the array, we can use,

```
```cpp
sort(a+3, a+5);
```
```

We have used a+5 for the second argument, which specifies that we want to sort to the last element in the array.

Now similar sort() function can work with vector container as shown in following program. This shows that STL algorithms are generic.

Program 13.12: Sorting of vector using sort algorithm

```
```cpp
#include <iostream>

#include <algorithm>

#include <vector>

using namespace std;

int main()
```
```