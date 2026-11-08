The definitions of the function templates above are based on fold expressions. C++11 supports variadic templates that can accept an arbitrary number of template arguments. Any number of template parameters is held by a so-called parameter pack. Additionally, with C++17, you can directly reduce a parameter pack with a binary operator. This reduction is called a fold expression14. In this example, the logical and && (line 7), the logical or || (line 10), and the negation of the logical or (line 13) are applied as binary operators. Furthermore, all, any, and none requires from their type parameters that they have to support the concept std::integral.

```
```
all(5, true, false): false
any(5, true, false): true
none(5, true, false): false
```
```

**Applying concepts onto a fold expression**

# #### 4.1.4.4.5 Overloading

std::advance15 is an algorithm of the Standard Template Library. It increments a given iterator by n elements. Based on the capabilities of the given iterator, a different advance strategy could be used. For example, a std::forward_list supports an iterator that can only advance in one direction, while a std::list supports a bidirectional iterator, and a std::vector supports a random access iterator. Consequently, for an iterator provided by a std::forward_list or std::list, a call to std::advance(iter, n) has to be incremented n times (see the structure of a std::list). This time complexity does not hold for a std::random_access_iterator provided by a std::vector. The number n can just be added to the iterator. A linear time complexity O(n) becomes, therefore, a constant complexity O(1). To distinguish iterator types, concepts can be used. The program conceptsOverloadingFunctionTemplates.cpp should give you the general idea.

**Overloading function templates on concepts**

```
```
// conceptsOverloadingFunctionTemplates.cpp

#include <concepts>
#include <iostream>
#include <forward_list>
#include <list>
#include <vector>

template<std::forward_iterator I>
void advance(I& iter, int n){
    std::cout << " forward_iterator" << '\n';
}
```
```