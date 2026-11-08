length of *q* to be 3. This means that the search finds the entry where most of the three-character substrings of the search pattern match an index entry.

If the index contains, for example, *Graum aus* and *Nagetierstamm*, then with the *Anagram* query you will find the latter, because both contain *NAG* and *AMM*, while the former does not have any three-letter group in common with *Anagram*. I don't want to say more about the algorithm as an example here, because it is really a side issue in this chapter. (While translating this chapter, I discovered that German is an excellent language to do q-grams with!)

If you call make all in the main directory, then the qwort.a library in src/lib/ and the programs in src/prog/ will be built one after the other.

The library here consists only of a minimal set of files: a header file that is to be delivered with the library, as well as the implementation files. These, in turn, consist of two *.cpp files, qwort.cpp and impl_multimap.cpp, as well as an internal *.hpp file, impl_multimap.hpp, which is not intended for delivery. Therefore, it is also located in src/lib/. If you deliver the library to a customer who uses a compiler compatible with yours, for static linking it is sufficient to deliver the qwort.a library file and on Windows qwort.lib together with the qwort.hpp header file. If you want to support dynamic linking too, you provide a qwort.so or qwort.dll library file.

> **The Header File Must Match the Library File**
> 
> It is crucial that you (and your customers) use the exact same header file that was used to build the library file when using your library. If you have different versions in use, the best thing that can happen is a compiler or linker error; in the worst case, the behavior will be unpredictable.

The main qwort.hpp header file is shown in Listing 11.1.

```
```cpp
# https://godbolt.org/z/e5GWbbq4Y
#ifndef QWORT_H // header guard
#define QWORT_H
#include <string>
#include <memory> // unique_ptr
namespace qw { // library namespace
    int version();
    namespace impl_multimap {
        class index_impl;
    }
    class index {
        using index_impl = impl_multimap::index_impl;
    public:
        index();
        ~index() noexcept; // needed for pimpl
```
```