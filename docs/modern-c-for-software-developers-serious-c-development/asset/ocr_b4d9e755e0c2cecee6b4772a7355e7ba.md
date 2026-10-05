```
FooFunction() { return {}; };
```

myFunction will return a default object of type Foo. For this statement to compile properly, Foo must have a default constructor that takes no arguments.

# std::initializer_list

Also See: Standard Library: initializer_list

Consider an array of integers in C++:

```
int array[5];
```

We can initialize this array with an initializer list:

```
int array[5] {0, 1, 2, 3, 4};
```

The expression in braces is called an initializer list.

The following initialization of a dynamically allocated array will also compile:

```
int *pArray = new int[5] {5, 4, 3, 2, 1};
```

Now consider the following array class:

```
#include <iostream>
#include <initializer_list>
class IntArray {
    private:
    int m_length;
    int *m_data;
    public:
    IntArray(): m_length(0), m_data(nullptr) { }
    IntArray(int length) : m_length(length)
```