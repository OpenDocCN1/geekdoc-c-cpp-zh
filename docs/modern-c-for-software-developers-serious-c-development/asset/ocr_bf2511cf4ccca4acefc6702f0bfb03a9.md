```
for (i = 0; i < v.size(); i++)
v[i] = (v[i].get_temperature() - 32) * 5 / 9;
cout << "Centigrade temperatures:\\n";

for (i = 0; i < v.size(); i++)
cout << v[i].get_temperature() << " ";

return 0;
n}
```

//output
ahrenheit temperatures:
73 76 87 85 83 85 76
Centigrade temperatures:
22 24 30 29 28 29 24

# List Containers

A list container implements a bidirectional, linear list. Unlike vectors which have random access, lists can only be accessed sequentially. Since lists are bidirectional, they can be accessed by traversing front to back or back to front. Lists have very fast insertion and deletion times but they have slower access times than vectors.

The declaration for a list template:

```
template <class T, class Allocator = allocator<T>> class list;
```

Here, T is the type of data stored in the list. The allocator is specified by Allocator, which defaults to the standard allocator.

We instantiate a list as follows:

```
include <list>

list<int> alist;             // create an empty list of integers
list<Foo> foo;              // create an empty list of Foo objects
```

The following list constructor constructs an empty list.