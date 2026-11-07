templates use a different syntax to indicate the type of data stored. Fourth, the vector class uses a different syntax to indicate the number of elements. Here are some examples:

```
```cpp
#include <vector>
...
using namespace std;
vector<int> vi;       // create a zero-size array of int
int n;
cin >> n;
vector<double> vd(n); // create an array of n doubles
```
```

We say that `vi` is an object of type `vector<int>` and that `vd` is an object of type `vector<double>`. Because vector objects resize automatically when you insert or add values to them, it’s okay for `vi` to start with 0 size. But for the resizing to work, you would use the various methods that are part of the vector package.

In general, the following declaration creates a vector object `vt` that can hold `n_elem` elements of type `typeName`:

```
```cpp
vector<typeName> vt(n_elem);
```
```

The parameter `n_elem` can be an integer constant or an integer variable.

# The array Template Class (C++11)

The vector class has more capabilities than the built-in array type, but this comes at a cost of slightly less efficiency. If all you need is a fixed-size array, it could be advantageous to use the built-in type. However, that has its own costs of lessened convenience and safety. C++11 responded to this situation by adding the array template class, which is part of the std namespace. Like the built-in type, an array object has a fixed size and uses the stack (or else static memory allocation) instead of the free store, so it shares the efficiency of built-in arrays. To this it adds convenience and additional safety. To create an array object, you need to include the array header file. The syntax is a bit different from that for a vector:

```
```cpp
#include <array>
...
using namespace std;
array<int, 5> ai;   // create array object of 5 ints
array<double, 4> ad = {1.2, 2.1, 3.43, 4.3};
```
```

More generally, the following declaration creates an array object `arr` with `n_elem` elements of type `typeName`:

```
```cpp
array<typeName, n_elem> arr;
```
```

Unlike the case for vector, `n_elem` can’t be a variable.

With C++11, you can use list-initialization with vector and array objects. However, that was not an option with C++98 vector objects.