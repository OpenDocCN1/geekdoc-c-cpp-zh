
## PART III: Advanced Topics

Part II mainly dealt with the obvious aspects of object-oriented programming, as you might know from Java or other languages. However, virtuality, inheritance, and even classes and methods are not the only way to achieve extensibility, encapsulation, and polymorphism. Arguably, you can also program in an object-oriented way in C if you put in the effort.

This part does not discuss whether other ways lead to object orientation, but it shows you possibilities beyond what has been discussed so far to design your programs and use other tools of the C++ language. You can omit elements of classical object-oriented programming and replace them with other means, achieving similar results while enjoying certain advantages.

I’ll start with the bridge to the ancestor of C++, the pointers and macros of C. Through the explanation of C++ templates, we eventually come to some elements of functional programming, from which C++ has borrowed a few things to enable expressive and flexible programs.

## Chapter 20: Pointers

### Chapter Terms

- **Pointer**: Variable that holds an address to data in the heap or stack.
- **Raw pointer**: Variable of type `Type *`, `Type const *` (constant value), `Type * const` (constant pointer), or `Type const * const` (both constant).
- **Heap memory or simply heap**: Place where data is stored that is requested dynamically—with `new`.
- **Stack memory or simply stack**: Memory location of objects that were created without `new`.
- **Automatic object**: An object created on the stack.
- **Dynamic object**: An object created on the heap.
- **Aliasing**: Referring to the same object from multiple variables.
- **Object ownership**: The variable that is responsible for removing a dynamic object via a pointer owns the object.
- **new and new[]**: Creating a dynamic object.
- **delete and delete[]**: Releasing a dynamically allocated object.
- **Smart pointers unique_ptr and shared_ptr**: Pointer types of the standard library following the RAII concept, which save you from explicit deallocation.
- **move**: Turning a named value into a temp-value, making it movable.
- **C-array**: A C-array contains multiple elements of the same type and is declared with square brackets.
- **Pointer arithmetic**: Addition, increment, and similar operations with raw pointers in a C-array.
- **C-array decay**: A C-array loses its size information when passed to a function.
- **Iterator**: The abstract concept of pointers, applied to standard containers.

Through character strings, you have already had a bit to do with pointers. You have always passed their literals around as `const char*`. And when you call `main` with arguments, the arguments are packed into a C-array of this type—that is, `const char*[]`. In this chapter, you will learn more about these constructs. They are not easy to understand but enable all sorts of useful things. However, you must use them correctly so that they do not cause you more trouble than they bring you benefits.

When you use pointers, the step to using dynamic memory is not far: `new` is the keyword here. However, I must immediately prevent a potential misunderstanding: if you use standard containers like `vector` and its relatives, then you are already using dynamic memory without realizing it. You get all the benefits but do not have to worry about the tricky details. Therefore, I would like to preface the following: in C++, you will not be able to avoid pointers in the medium term, but you should always check the alternatives first. If you even want to handle dynamic memory yourself, then do not use raw pointers for its ownership, but use the `unique_ptr` and `shared_ptr` smart pointers.

### 20.1 Addresses

At runtime, every “thing” must be stored somewhere. The most important things here are variables. In this sense, parameters are also variables. Other things that might not be so obvious that they need to be stored somewhere are functions and methods. In C++, functions are also just variables of a certain (complicated) type. For comparison: things that only the compiler needs and that are no longer present at runtime do not have an address, such as types themselves and the `*.cpp` files that are translated into the program. You cannot query the address of `int` or `MyType`, nor of `program.cpp`.

Every object must be stored somewhere while the program is running. For this, there is the *memory*. Technically speaking, everything that resides in memory is an *object*, and if this object has a name, it is a *variable*. You can think of memory as a street with houses, where each house can store an object. Your computer only knows this one street, so it only remembers the house number of the object. These addresses are often given in hexadecimal form. The exact form does not matter here; it also varies across different systems. For the examples in this chapter, `0xab08` and similar will represent addresses: starting with `0x`, followed by four or eight characters from `0123456789abcdef` (16 different ones—hence, hexadecimal).

However, for each type, there is a corresponding additional type that represents not the value itself, but the address of a value of that type. For example, if you define a variable `int value = 42;`, then `value` has the type `int`. The address of `value` has the type `int*`. You can now define a new variable of this additional type that holds the address of `value`:

```cpp
int value = 42;
int* pValue = &value;
```

In Figure 20.1, you can see how this looks in memory.

![](img/74416a2c3cfc2d60ea17cab4deeb9a13_521_0.png)

**Figure 20.1** You can think of memory locations as houses on a street.

The definition of `pValue` in the second line requires an explanation. Because `pValue` is not an `int`, `int* pValue = value;` would be incorrect; you do not need the *value* from `value`, but its *address*. And this is exactly what the *unary address operator* `&` before the variable name does. `&value` gives you the address of `value`. Because `value` is of type `int`, `&value` is of type `int*`. The assignment of `&value` to `int* pValue` is therefore correct.

### 20.2 Pointer

The exciting thing now is that with `*pValue` you have an alternative way to access the value in `value`. When you apply the *unary dereference operator* `*` to `pValue`, it points to the memory with the 42. If you write something there, you also change the value of `value`. With `*pValue`, you have an *alias* for `value`:

```cpp
*pValue = 18;
cout << value << "\n"; // Output: 18
```

If I may stick with the image of the street and the houses, the following happens: With `pValue` you go to its house (`0xab02`), look inside, and find the address `0xab04`. With the dereference operator `*` you follow the arrow and arrive at the house of `value`. The assignment `= 18` writes the new value to the location in memory—that is, at `value`.

This is not much different from what you could have done with references:

```cpp
// https://godbolt.org/z/4536hxvEK
int value = 42;
int& valueRef = value;   // Reference; no address operator & needed
valueRef = 18;            // no dereference operator * needed
cout << value << "\n";  // Output: 18
```

Here, the address operator `&` and dereference operator `*` are omitted because the `valueRef` name itself is an alias for the original variable `value`.

But there is one thing pointers can do that references cannot: you can assign a new address to a pointer.

```cpp
// https://godbolt.org/z/7GEWYeoC9
#include <vector>
#include <iostream>
using std::vector; using std::cout; using std::ostream;
ostream& printVector(ostream& os, const vector<int>& arg) { // Helper function
    for(int w : arg) os << w << " "; return os;
}

int main() {
    vector<int> values{};
    values.reserve(50);                 // Guarantee space for 50 values
    int *largest = nullptr;             // First, assume it is a special value
    for(int w : { 20, 2, 30, 15, 81, 104, 70, 2, }) {
        values.push_back(w);
        if(!largest || *largest < w) {  // Dereference to value
            largest = &(values.back()); // Remember new address; hence not nullptr
        }
    }
    printVector(cout, values) << "\n"; // Output: 20 2 30 15 81 104 70 2
    // largest now contains the address of 104:
    *largest = 999;                     // Dereference; also overwrite value
    printVector(cout, values) << "\n"; // Output: 20 2 30 15 81 999 70 2
}
```

**Listing 20.1** Pointers can be assigned new addresses during their lifetime.

First, I initialize the vector `values` here without elements. The pointer variable `int* largest` should always point to the largest element in the vector. Because the vector is still empty, I initialize the variable with the special `nullptr` value, which means “points nowhere.”

Then I add a few arbitrary numbers to the vector one by one. As soon as I have done that, I always check with `if(...)` whether the new value is greater than what `*largest` currently holds. Now it gets dangerous, because `largest` can contain the special value
