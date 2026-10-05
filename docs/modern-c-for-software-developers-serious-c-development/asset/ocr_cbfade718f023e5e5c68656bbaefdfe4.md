```
==, <, <=, !=, >, >=
```

The index operator [ ] implements class random access to the elements of a vector.

The Vector container has numerous class member functions. The size function returns the current size of the vector. The begin function returns iterator to the start of the vector. The end function returns an iterator to the end of the vector.

The push_back function pushes a value onto an end of a vector. If necessary, the vector is increased in length to accommodate the new element. pop_back removes the last element of the vector. insert inserts an element at a specified position in the vector. We can remove all the elements in a vector with clear. empty() is a predicate that tests if a vector is empty.

The following example demonstrates a vector class:

```
// Demonstrate a vector
#include <iostream>
#include <vector>

using namespace std;

int main ()
{
    // create an integer vector of length 10
    vector<int> v(10);
    size_t i;

    // display the size of v
    cout << "Size = " << v.size() << endl;

    // assign values to the elements of the vector
    for (i = 0; i < 10; i++) v[i] = i;

    // display contents of the vector
    cout << "Current Contents:\n";
    for (i = 0; i < v.size(); i++) cout << v[i] << " ";
    cout << "\n\n";

    // push more values onto the end of the vector,
    // the vector will grow as needed
```