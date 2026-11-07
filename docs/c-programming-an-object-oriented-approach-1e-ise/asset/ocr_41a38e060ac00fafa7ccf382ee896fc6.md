![](bbox=[0.355, 0.089, 0.809, 0.187])

# **Figure 19.16** Graphical representation of set union

Figure 19.16 shows union operations applied to *first* and *second* sets. The result is the shaded area. The union is a set that includes all elements in *first* and *second*.

Program 19.29 shows how we can apply the union operation on the two sets (*first* and *second*).

# **Program 19.29** Finding the union of two sets

```
```cpp
/***************************************************************
 * A program that finds the union of two sets                    *
 ***************************************************************/
#include <set>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

// Print function
void print(int value)
{
    cout << value << " ";
}

int main()
{
    // Creation of the first set
    set <int> first;
    first.insert(10);
    first.insert(19);
    first.insert(14);
    first.insert(17);
    first.insert(13);
    cout << "Elements of first set" << endl;
    for_each(first.begin(), first.end(), print);
    cout << endl << endl;
    // Creation of the second set
    set <int> second;
    second.insert(16);
    second.insert(14);
```
```