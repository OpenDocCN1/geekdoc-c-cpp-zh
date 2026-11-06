```
```cpp
bool RandomPtrIterator<Class, BaseIterator, Type>::operator<(
            RandomPtrIterator const &other) const
{
    return **d_current < **other.d_current;
}
```
```

Some additional examples: operator*, defined in the class iterator as

```
```cpp
inline std::string &StringPtr::iterator::operator*() const
{
    return **d_current;
}
```
```

is now implemented as:

```
```cpp
template <typename Class, typename BaseIterator, typename Type>
Type &RandomPtrIterator<Class, BaseIterator, Type>::operator*() const
{
    return **d_current;
}
```
```

The pre- and postfix increment operators are now implemented as:

```
```cpp
template <typename Class, typename BaseIterator, typename Type>
RandomPtrIterator<Class, BaseIterator, Type>
&RandomPtrIterator<Class, BaseIterator, Type>::operator++()
{
    ++d_current;
    return *this;
}
template <typename Class, typename BaseIterator, typename Type>
RandomPtrIterator<Class, BaseIterator, Type>
RandomPtrIterator<Class, BaseIterator, Type>::operator++(int)
{
    return RandomPtrIterator(d_current++);
}
```
```

Remaining members can be implemented accordingly, their actual implementations are left as exercises to the reader (or can be obtained from the cplusplus.yo.zip archive, of course).

Re-implementing the class StringPtr developed in section 21.13.1 is not difficult either. Apart from including the header file defining the class template RandomPtrIterator, it only requires a single modification. Its iterator typedef must now be associated with a RandomPtrIterator. Here is the full class interface and the class's inline member definitions:

```
```cpp
#ifndef INCLUDED_STRINGPTR_H_
#define INCLUDED_STRINGPTR_H_

#include <vector>
#include <string>
#include "iterator.h"

class StringPtr: public std::vector<std::string *>
{
    public:
        typedef RandomPtrIterator
        <
```
```