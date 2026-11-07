The `emplace_back()` method is a variadic template with a function parameter pack as its argument:

```
```cpp
template <class... Args> void emplace_back(Args&&... args);
```
```

The three arguments 8.2, 2.8, and 3 are packed into the args parameter. These parameters are passed along to the allocation function, which then can unpack the parameters and use the Items constructor with three arguments (#2) instead of the default constructor (#1). That is, it can use Items(args...), which, in this example, expands to Items(8.2, 2.8, 3). Thus, the desired object is constructed in place in the vector rather than at a temporary location and then copied to the vector.

The STL uses this technique with several emplacement methods.

# Members Common to All or Most Containers

All containers define the types in Table G.1. In this table, X is a container type, such as vector<int>, and T is the type stored in the container, such as int. The examples following the table clarify the meanings.

Table G.1 Types Defined for All Containers

| Type | Value |
|------|-------|
| X::value_type | T, the element type. |
| X::reference | T &. |
| X::const_reference | const T &. |
| X::iterator | Iterator type pointing to T, behaves like type T *. |
| X::const_iterator | Iterator type pointing to const T; behaves like type const T *. |
| X::difference_type | Signed integral type used to represent the distance from one iterator to another (for example, the difference between two pointers). |
| X::size_type | Unsigned integral type size_type can represent size of data objects, number of elements, and subscripts. |

The class definition uses a typedef to define these members. You can use these types to declare suitable variables. For example, the following code uses a roundabout way to replace the first occurrence of "bemus" in a vector of string objects with "bogus" in order to show how you can use member types to declare variables:

```
```cpp
using namespace std;
vector<string> input;
string temp;
while (cin >> temp && temp != "quit")
    input.push_back(temp);
vector<string>::iterator want=
```
```