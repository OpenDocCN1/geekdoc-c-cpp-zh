Here is an example of the sort algorithm:

# Example 10.8: Example of sort algorithm.

```
//10_8.cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <functional>
using namespace std;

int main()
{
    int A[] = {1, 4, 3, 2, 5};
    const int N = sizeof(A)/sizeof(int);
    vector<int> coll(A,A+N);
    ostream_iterator<int> output(cout, " ");

    cout << "Vector coll contains: " << output << endl;
    copy(coll.begin(), coll.end(), output); //first order to call
    sort(coll.begin(), coll.end());
    cout << "\nAfter sorted in ascending order coll contains: " << output << endl;
    copy(coll.begin(), coll.end(), output); //elements in coll after ascending sort
    sort(coll.begin(), coll.end(),greater<int>()); // //second way, to use standard functional object
    cout << "\nAfter sorted in descending order coll contains: " << output << endl;
    copy(coll.begin(), coll.end(), output); //elements in coll after descending sort

    cout<<endl;
}

```

Results:

| Vector coll contains: 1 4 3 2 5 |
After sorted in ascending order coll contains: 1 2 3 4 5 |
After sorted in descending ordercoll contains: 5 4 3 2 1 |

# 10.4.2 Nonmutating Sequence Algorithms

Nonmutating Sequence Algorithms do not modify the elements of the input containers, as as algorithms for finding an element in a container, checking whether sequences are equal, and counting the occurrence of elements.