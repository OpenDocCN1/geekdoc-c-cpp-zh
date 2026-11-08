
```cpp
int main()
{
    std::vector vdata { 2, 0, 15, 12 };
    printBinary(std::cout, vdata) << "\n";
    // Output: 0010 0000 1111 1100
    std::set sdata { 2, 0, 12, 15 };
    printBinary(std::cout, sdata) << "\n";
    // Output: 0000 0010 1100 1111
    int adata[] = { 0,1,2,13,14,15 };
    printBinary(std::cout, adata) << "\n";
    // Output: 0000 0001 0010 1101 1110 1111
}
```

**Listing 23.9** Pass your own algorithm ranges as arguments, not the container.

With `auto` as the second parameter, you have defined a template. Before C++17, you had to put `template<typename T>` before the function and `T&&` for the parameter—as described in the previous section. The `&&` ensures that you can pass both values directly from variables and temp-values from expressions. Before `auto` is the `std::ranges::input_range` concept. It works without it, but you tell the compiler and the user of the function a lot when you write it down. In particular, the compiler's error messages will be better. You can find more about ranges as parameters in Chapter 25, Section 25.6, under the subheading “Ranges as Parameters (and More).”

The `printBinary()` function converts all elements of the range into a `bitset<4>`, which is then printed. The conversion to `bitset` naturally only works if the container from which the iterators originate contains integer types, which is the case here with `int`. If you try `printBinary()` with a container that contains `string` or `double`, the compiler will report an error exactly where the conversion is attempted with `std::bitset<4> x(elem);`.

As for the type of container, using ranges is flexible. Try it with a vector like `vdata`, and you will get the content output as binary numbers. With a set like `sdata`, the elements are also sorted—a property of the set class. And because raw pointers are just a certain form of iterators, you can even call the `printBinary()` function with a C-array like `adata`. Ranges work for standard containers as well as for C-arrays.

Note that I have omitted the template arguments for vector data and set data here and let the compiler deduce them, which has been possible since C++17.

If you are programming for a compiler that does not yet support ranges, you need to “unpack” the range—that is, get the two iterators and call the function with the iterators.

```cpp
// https://godbolt.org/z/13eMxKTfj
#include <iostream>
#include <vector>
#include <set>
#include <bitset>

template<typename IT>
std::ostream& printBinary(std::ostream& os, IT begin, IT end)
{
    for(IT it=begin; it != end; ++it) {
        std::bitset<4> x(*it); // Copy number into bitset
        os << x << " ";
    }
    return os;
}
int main()
{
    std::vector<int> vdata { 2, 0, 15, 12 };
    printBinary(std::cout, vdata.cbegin(), vdata.cend()) << "\n";
    // Output: 0010 0000 1111 1100
    std::set<int> sdata { 2, 0, 12, 15 };
    printBinary(std::cout, sdata.begin(), sdata.end()) << "\n";
    // Output: 0000 0010 1100 1111
    int adata[] = { 0,1,2,13,14,15 };
    printBinary(std::cout, std::begin(adata), std::end(adata)) << "\n";
    // Output: 0000 0001 0010 1101 1110 1111
}
```

**Listing 23.10** Pass your own algorithm iterators as arguments, not the container.

Specifically, TYPE is instantiated by printBinary() in this example with three different types:

- For `vdata.cbegin()`, TYPE is a `vector<int>::const_iterator`, as this is what the function `cbegin()` returns.
- For `std::begin(sdata)`, it is a `set<int>::iterator`, as that is the return type of `set<int>`. You would have gotten a `const_iterator` if you had declared `sdata` const.
- For `std::begin(adata)`, TYPE will be a raw pointer `int*`. The loop in the `printBinary()` function, which looks like it specializes in iterators, also works on raw pointers—precisely because they are just a form of iterators.

I also did not use `auto` for the parameter here, did not specify a concept, and did not use template argument deduction. This is now C++14 compatible.

Writing your own functions on containers in this manner increases the flexibility of your program in the long run. Of course, this is not suitable everywhere. So long as you only read the elements in the range, everything will definitely work. Here, we only let the loop run forward. Maybe you want to write an algorithm that accesses the elements of the range backward or even randomly. Then it may be that some containers do not cooperate with your function or behave undesirably. A `list` does not allow random access to its elements. With the choice of the right range concept, you can document that.

So long as you keep this in mind, you are definitely on the safe side for functions that only read. If you also need write access, you need to be a bit more cautious. When you describe an element with a new value, you must consider that, for example, a `set` wants to keep its elements sorted—and it will do so, causing the order of elements to change and thus the range as well.

### 23.2.2 Example: Information about Numbers

In the following example, you will not only see the use of a function template but also that there is a very interesting helper template, `numeric_limits<>`. With it, you can find out all sorts of useful internals and use them in your program. If you want to initialize a vector large enough to hold all possible values of `unsigned short`, you can do it like this:

```cpp
const auto sz = std::numeric_limits<unsigned short>::max();
std::vector<string> dictionary(sz);
```

If the `unsigned short` type on your system has a width of 16 bits, then `unsigned short` variables can hold values from 0 to 65535. The `sz` variable takes this value, and the vector `dictionary` is initialized with this size.

A few examples of what else you can find out using `numeric_limits` are shown in Listing 23.11.

```cpp
// https://godbolt.org/z/t83Yeon7r
#include <iostream>              // cout
#include <limits>                // numeric_limits
template<typename INT_TYP>       // Template with type argument
void infos(const char* name) {
    using L = typename std::numeric_limits<INT_TYP>; // rename for brevity
    std::cout
        << name
        << " number of bits:" << L::digits      // Bits without sign bit
        << " sign:" << L::is_signed             // stores sign?
        << " min:"<< (long long)L::min()        // smallest possible value
        << " max:"<< (long long)L::max()        // largest possible value
        << "\n";
}
int main() {
    infos<signed char>("char");              // smallest int type
    infos<short>("short");
    infos<int>("int");
    infos<long>("long");
    infos<long long>("long long");            // largest int type
}
```

**Listing 23.11** How to find the range of integer types.

Although this example is only designed for integer types, there are also many information functions for the float and double floating-point types.

### What Is “typename”?

> So far, you have only seen typename for template parameters—for example, before functions in `template<typename T>`. In such cases, you can also use class instead: `template<class T>` means exactly the same thing.
>
> Since C++20, you can also use the name of a concept instead of typename to restrict the type of a template parameter. If infos is supposed to work only for integer types, use the `std::integral` concept from the `<concepts>` header instead of typename.
>
> Outside of angle brackets, a typename appears exactly when you are writing a template and a type you are using is itself a template type in which you are using one of your template parameters. You can see this in Listing 23.11 at `typename std::numeric_limits<INT_TYP>`. Then you need the additional word typename before the name of the template type you are using. Otherwise, the compiler cannot know, before you assign a value/type to `INT_TYP`, whether `numeric_limits<...>` is a variable, a type, or something else. You then have to tell it: “Hey, by the way, this is a type.”

## 23.3 A Class as a Function

So far, you can do two things with a function: you can define it, and you can call it. It becomes exciting and truly flexible only when you consider functions not just as a piece of outsourced program code but as objects like all other C++ objects. When you pass a function as a parameter, receive it as a return value, or simply store it in a variable for later use, you are using functions as objects.

I'll start with a very simple example. Say you want to write something that performs either an addition or a multiplication operation depending on a parameter. In the context of this chapter, I would like to call the thing that sometimes performs one operation and sometimes another a procedure to conceptually distinguish it from the variable function (addition or multiplication).
