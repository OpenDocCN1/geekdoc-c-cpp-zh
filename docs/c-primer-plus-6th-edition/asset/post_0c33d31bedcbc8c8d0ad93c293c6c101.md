
# Appendix G The Standard Template Library Methods and Functions

list, with each item, other than the last, linked to the next item. It provides a more compact, by more limited, alternative for list.

Like set and the other associative containers, the unordered associative containers allow fast data retrieval through the use of keys. The difference is that the associative containers use trees as the underlying data structure, whereas the unordered associative containers use hash tables.

## Changes to C++98 Containers

C++11 brings three main changes to the container class methods.

First, the addition of rvalue references makes it possible to provide move semantics (Chapter 18, "Visiting with the New C++ Standard") for containers. Accordingly, the STL now provides move constructors and assignment operators for containers. These methods take an rvalue reference.

Second, the addition of the initializer_list template class (Chapter 18) has led to constructors and assignment operators that accept an initializer_list argument. This makes code like the following:

```
vector<int> vi(100, 99, 97, 98);
vi = {96, 99, 94, 95, 102};
```

Third, the addition of variadic templates and function parameter packs (Chapter 18) makes emplacement methods possible. What does this mean? Like move semantics, emplacement is a means to increase efficiency. Consider the following code snippets:

```
class Items {
    double x;
    double y;
    int m;
public:
    Items();                // #1
    Items(double xx, double yy, int mm); // #2
};
```

```
vector<Items> vt(10);
t.push_back(Items(8.2, 2.8, 3)); //
```

The call to insert() causes the memory allocation function to create a default Items object at the end of the vt. Next, the Items() constructor creates a temporary Items object; this object is copied to a location at the front of the vector vt and then the temporary object is deleted. With C++11, you can do this instead:

```
vi.emplace_back(8.2, 2.8, 3);
```

## Members Common to All or Most Containers

The emplacement_back() method is a variadic template with a function parameter pack as its argument:

```
template<class...> void emplace_back(Args&... args);
```

The three arguments 8.2, 2.8, and 3 are packed into the args. These parameters are passed along with the allocation function, which then unpack the parameters and use the Items constructor with three arguments (#2) instead of the default constructor (#1). That is, it can use Items(args...), in which this expands to Items(8.2, 2.8, 3). Thus the desired object is constructed in place the vector rather than at a temporary location and copied to the vector.

The STL uses this technique with several emplacement methods.

## Members Common to All or Most Containers

All containers define the types in Table G.1. In this table, x is a container type, such as vector<int>, and T is the type stored in the container, such as int. The examples following table clarifies the meanings.

### Table G.1 Defined for All Containers

| Type | Value |
|---|---|
| X::value_type | T, the element type. |
| X::reference | T & |
| X::const_reference | const T & |
| X::iterator | Iterator type pointing to T; behaves like type T |
| X::const_iterator | Iterator type pointing to const T; behaves like const T * |
| X::difference_type | Signed integer type to represent the distance from one iterator to another (for, the difference between two pointers). |
| X::size_type | Unsigned integer type size_type can represent size of data objects, number of elements, and subscripts. |

The class definition uses typedef to define these members. You can use code a roundabout way to replace the first occurrence of "bonus" in a vector of string objects with "bogus" in order to show how you can use member types to declare variables:

```
using namespace std;
vector<string> input;
string temp;
while (cin >> temp && temp != "quit")
input.push_back(temp);
vector<string>::iterator want =
```

```
find(input.begin(), input.end(), string("bonus"));
if (want != input.end())
{
    vector<string>::reference r = *want;
    r = "bonus";
}
```

This code makes r a reference to the element in input to which want points. Similarly, continuing with the preceding example, you can write code like the following:

```
vector<string>::value_type s1 = input[0]; // s1 is type string
vector<string>::reference s2 = input[1]; // s2 is type string &
```

This results in s1 being a string object that is a copy of input[0] and s2 being a reference to input[1]. In this example, given that you already know the template is of string type, it would be simpler to write the following code, which is equivalent in its effect:

```
string s1 = input[0]; // s1 is type string
string s2 = input[1]; // s2 is type string &
```

However, the elaborate types from Table G.1 can also be used in more general code where the type of container and element are generic. For example, suppose you want a function that takes its argument as a reference to a container and returns the smallest item in the container. This assumes that the < operator is defined for the value type used to instantiate the template and that you don't want to use the STL min_element algorithm, which uses an iterator interface. Because the argument could be vector<int> or list<string> or deque<double>, you use a template parameter, such as Bag, to represent the container (That is, Bag is a template type that might be instantiated as vector<int>, list<string>, or some other container type). So the argument for the function is const Bag &. What would be the return type? It should be the value type for the container—that is, Bag::value_type. However, at this point, Bag is a template parameter, and the compiler has no way of knowing what the value_type member is. You can use the typename keyword to clarify that a class member is a typedef:

```
vector<string>::value_type st; // vector<string> a defined class
typename Bag::value_type m; // Bag as an ended typedef type
```

For the first definition, the compiler has access to the vector template definition, which states that value_type is a typedef. For the second definition, the typename provides that, whatever Bag may turn out to be, the combination Bag::value_type is the name of a type. These considerations lead to the following definition:

```
template <typename Bag>
typename Bag::value_type min(const Bag & b)
{
```

```
typename Bag::const_iterator it;
typename Bag::value_type m = *b.begin();
```

```
for (it = b.begin(); it != b.end(); ++it)
  if (*it < m)
    m = *it;
return m;
```

You can use this template function as follows:

```
vector<int> temperatures;
// input temperature values into the vector
int coldest = min(temperatures);
```

The Temperatures parameter would cause Bag to be evaluated as vector<int> and typename Bag::value_type to be evaluated as vector<int>::value_type, which in turn, is int.

All containers have the member functions or operations listed in Table G.2. Again, X is a container type, as vector<int>, and T is the stored in the container, such as int. Also a and b are values of x, u is an identifier, and r is a non-const value of type x, and rv is a non-const value of type x. The move operations were added with C++11.

### Table G.2 Operations Defined for All Containers

| Operation | Description |
|---|---|
| X u | Constructs an empty object u. |
| X() | Constructs an empty object. |
| X(a) | Constructs a copy of object a. |
| X u(a) | u is a copy of a (copy constructor). |
| X u = a; | u is a copy of a (copy constructor). |
| r = a | r equals the value of a (copy assignment). |
| X u(rv) | u equals the value that rv had before construction (move constructor). |
| X u = rv; | u equals the value that rv had before construction (move constructor). |
| a = rv | a equals the value that rv had before construction (move assignment). |
| begin() | Returns an iterator to the first element. |
| end() | Returns an iterator to the end. |
| cbegin() | Returns a const iterator to the first element. |
| cend() | Returns a const iterator to the end. |
| size() | Returns the number of elements. |
| maxsize() | Returns the size of the largest possible container. |
| empty() | Returns true if the container is empty. |
