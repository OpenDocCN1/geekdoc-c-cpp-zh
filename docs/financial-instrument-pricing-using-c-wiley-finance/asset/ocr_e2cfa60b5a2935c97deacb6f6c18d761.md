# 10.6.2 boost::array<> and std::array<>

The STL vector<T> container provides the semantics of dynamic arrays. The number of elements in this class is variable and it is possible to append elements to it at run-time. In some applications, however, we may wish to work with arrays whose size is known at compile-time. To this end, the Boost.Array library is one solution. It consists of a class template array<V,N> having two template parameters, one parameter N for the size of the array and the other parameter V for the underlying data type. The interface has the following functionality:

+   - Array assignment.
+   - Accessing the elements of an array using the operator [] and the at() member function.
+   - Iterators.
+   - Member functions to retrieve the first and last elements of an array.
+   - We can compare arrays using the binary operators ==, !=, <, >, <=, >=.
+   - We can exchange elements of two arrays using the swap() member function.

We take some simple examples. First, we create an array of long and we initialise its elements:

```
const int N = 4;
boost::array<long, N> myArr = {1, 2, 3, 4};
```

We can now print the elements of the array by using an iterator and the indexing operator:

```
// Using iterators
boost::array<long, N>::const_iterator it;
for (it = myArr.begin(); it != myArr.end(); ++it)
{
    cout << *it << endl;
}

// Indexing operator
for (long i = 0; i < myArr.size(); ++i)
{
    cout << myArr[i] << endl;
}
```

It is also possible to initialise an array as follows:

```
const int M = 2;
boost::array<string, M> myStringArr;
myStringArr[0] = "Hello";
myStringArr[1] = "World";
```

We now take an array that models a simple fixed-size polyline consisting of points. The elements of the array consist of instances of class Point whose interface is: