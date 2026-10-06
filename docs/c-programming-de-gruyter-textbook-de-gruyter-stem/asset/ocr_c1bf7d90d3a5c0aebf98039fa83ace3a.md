# 10.4.5 Numerical Algorithms

There are four generic numerical algorithms; Table 10.7 lists numerical algorithms in STL.

Here is an example of numerical algorithms in STL.

Example 10.12: An example of numerical algorithms.

```
//10_12.cpp
#include <iostream>
#include <numeric>
#include <functional>
#include <vector>
using namespace std;

int main() {
    int iarray[]={1,2,3,4,5};
    vector<int> ivector(iarray,iarray+sizeof(iarray)/sizeof(int));

    // Accumulation of elements
    cout<<accumulate(ivector.begin(), ivector.end(),0)<<endl;

    // Inner product of vectors
    cout<<inner_product(ivector.begin(), ivector.end(), ivector.begin(), 10)<<endl;

    // Sum of elements in a vector
    partial_sum(ivector.begin(), ivector.end(), ostream_iterator<int>(cout, " "));
    cout<<endl;

    // Difference of adjacent elements in a vector
}
```

Tab. 10.7: STL Numerical Algorithms.

| Name | Function |
| --- | --- |
| accumulate | Calculate the sum of all elements in a sequence |
| partial_sum | Add parts of the elements in a sequence, save them into another sequence |
| adjacent_difference | Calculate the differences of adjacent elements in a sequence, save them into another sequence |
| inner_product | Add the corresponding elements of two sequences (inner product of vectors) |