# 20.6. NAMESPACES

```
cout << max({5, 4, 3, 2, 1}) << '\n';
cout << max({3, 4, 5, 2, 1}) << '\n';
cout << max({5, 2, 3, 4, 5}) << '\n';
cout << max({5, 5, 4, 5, 2, 5}) << '\n';
cout << max({5}) << '\'n';
cout << max({5, 5, 5, 5, 5}) << '\n';
}
```

Notice the blanket using namespace std directive that makes all the function and type names in the std namespace available to this program. This has not been our common practice so far, but you frequently will encounter this approach in published C++ code. This program works correctly, however, as it prints the following:

```
true
false
true
--------------------------------
1
1
1
2
3
1
5
```

The C++ standard library contains a function named is_sorted, declared in the <algorithm> header. The standard is_sorted performs the same task as this is_sorted, except that the standard function, striving to be as generic as possible, accepts two iterators instead of the container itself. In preparation to replace our is_sorted function with the standard is_sorted function, we add the following directive to the top of the code with the other #includes:

```
#include <algorithm>
```

If we compile and run our program with this addition, we get no errors or warnings, and the program prints the following:

```
true
false
true
--------------------------------
5
5
5
5
5
5
5
5
```

Observe that our max function behaves very differently after this slight change. In fact, the code that executes for the max invocations is not the code in Listing 20.52 (maxvector.cpp) but rather the max function in the standard library! This is because a call such as

```
max({1, 2, 3, 4, 5})
```