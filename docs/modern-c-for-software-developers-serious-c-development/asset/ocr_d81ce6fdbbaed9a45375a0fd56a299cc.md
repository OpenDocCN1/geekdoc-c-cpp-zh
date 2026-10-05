```
for (i = 0; i < 5; i++) v.push_back(i + 10);
```

```
// display the current size of v
cout << "Vector size now = " << v.size() << endl;
```

```
// display contents of the vector
cout << "Current contents:\n";nfor (i = 0; i < v.size(); i++) cout << v[i] << " " ";
cout << "\n";
```

```
// change the contents of the vector
for (i = 0; i < v.size(); i++) v[i] = v[i] + 100;
```

```
cout << "Modified vector contents:\n";nfor (i = 0; i < v.size(); i++) cout << v[i] << " " ";
cout << endl;
```

```
return 0;
}
```

```
// output
size = 10
Current Contents:
0 1 2 3 4 5 6 7 8 9
Vector size now = 15
Current contents:
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14
Modified vector contents:
100 101 102 103 104 105 106 107 108 109 110 111 112 113 114
```

# Accessing a Vector Through an Iterator

Arrays and pointers are closely related in C and C++. An array element can be accessed either through it's index or through a pointer. The STL we also access the data members of a vector with an index or through the use of an iterator:

```
// Access the elements of a vector through an iterator
#include <iostream>
#include <vector>
using namespace std;
```

```
int main() {
    vector<int> v(10); // create an int vector of length 10
    // create an iterator to a (generic) int vector
    vector<int>::iterator p = v.begin();
```