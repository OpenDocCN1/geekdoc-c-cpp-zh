# 2.2 Variables and initialization    CHAPTER 02: LANGUAGE USABILITY ENHANCEMENTS

In the above code, we can see that the itr variable is defined in the scope of the entire main(), which causes us to rename the other when a variable needs to traverse the std::vectors again. C++17 eliminates this limitation so we can do this in if(or switch):

```
if (const std::vector<int>::iterator itr = std::find(vec.begin(), vec.end(), 3);
    itr = vec.end()) {
    *itr = 4;
}
```

It is similar to the Go?

# Initializer list

Initialization is a very important language feature, the most common one is when the object is initialized. In traditional C++, different objects have different initialization methods, such as ordinary arrays, PODs (Plain Old Data, classes without constructs, destructors, and virtual functions) Or struct type can be initialized with {}, which is what we call the initialization list. For the initialization of the class object, you need to use the copy constructor, or you need to use (). These different methods are specific to each other and cannot be generic. E.g:

```
#include <iostream>
#include <vector>
```

```
class Foo {
public:
    int value_a;
    int value_b;
    Foo(int a, int b) : value_a(a), value_b(b) {}
};

int main() {
    // before C++11
    int arr[3] = {1, 2, 3};
    Foo foo(1, 2);
    std::vector<int> vec = {1, 2, 3, 4, 5};

    std::cout << "arr[0]:" << arr[0] << std::endl;
    std::cout << "foo:" << foo.value_a << ", " << foo.value_b << std::endl;
    for (std::vector<int>::iterator it = vec.begin(); it != vec.end(); ++it) {
        std::cout << *it << std::endl;
    }
}
```