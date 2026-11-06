
- **Nullable references:** Handles instances in which a pointer doesn’t point to anything
- **Avoiding copies:** Uses a single copy of an object instead of creating multiple copies, which reduces the risk of errors

As your knowledge of C++ increases, you soon discover that these are critical application needs, so replacing the raw pointer will be quite difficult. Fortunately, you don’t have to use the new C++20 features immediately, even if you’re using a C++ compiler. You control whether your application uses the new approach through compilation directives:

```cpp
#feature <no_pointers> //opt-in to no pointers
#feature <cpp20>       //opt-in to all C++20 features
```

Consequently, you don’t have to worry about your existing code suddenly breaking. The idea is to make the transition from raw pointers to something better as smooth and transparent as possible. Given the realities of C++ development, you likely will see some sort of legacy support for a long time. However, to move forward, you must adapt to the new realities of pointers in C++.

## Considering the issues

At this point, you might wonder why raw pointers are such a problem. After all, a pointer is simply an address in memory that looks something like 0x9caef0. The value it contains is the address, and by dereferencing the pointer, looking at the address to which it points, you see the value that the pointer references. It’s just like the address for your house. You send mail to the address, but the address isn’t your house — it’s simply a pointer to your house.

At this point, it doesn’t sound as if using pointers would be a problem, despite being a bit convoluted. The reason for using pointers in the first place is to avoid carrying large objects around in your code. You can leave the object, like a house, sitting in one place and simply point to it as needed. Imagine having to carry your house around with you. Besides having a horrible backache, doing so would be inconvenient and make your house harder to find. Instead, you give someone who wishes to mail you a letter or visit you in your home the address. Early applications had to use every tiny bit of memory and CPU processing cycles efficiently or face performance issues. Pointers allowed early applications to perform well by simply pointing at big objects in memory, rather than passing them around.

## PLACING A HEX ON C++

Sooner or later in your computer programming, you encounter a strange way of notating numbers on the computer. This strange way is called *hexadecimal*, or sometimes just *hex*. In C++, you can recognize a hex number because it starts with the characters 0x. These characters aren’t actually part of the number; they just notate it in the same way as double quotes denote a string. Whereas the usual decimal numbers consist of the digits 0, 1, 2, 3, 4, 5, 6, 7, 8, and 9, a hex number consists of these digits plus six more: A, B, C, D, E, and F. That makes a total of 16 digits. A good way to picture counting with regular decimal numbers is to use the odometer in a car, which (if you’re honest) goes only forward, not backward. It starts out with 00000000 (assuming eight digits, which is a lot). The rightmost digit runs from 0 through 9, over and over. When any digit reaches 9 and all digits to the right of that are 9, the next digit to the left goes up by 1. For example, when you reach 00000999, the next digit to the left goes up by 1 as each 9 goes back to 0, to get 00001000.

With hex numbers, you count this same way, except that instead of stopping at 9 to loop back, you then go to A, and then B, and then up to F. And then you loop back. So the first 17 hex numbers are, using eight digits, 00000000, 00000001, 00000002, 00000003, 00000004, 00000005, 00000006, 00000007, 00000008, 00000009, 0000000A, 0000000B, 0000000C, 0000000D, 0000000E, 0000000F, 00000010. Notice that when you hit F at the end, the number wraps around again, adding 1 to the next digit to the left. When working with hex numbers, you may see such numbers as 0xAAAA0000 and 0x0000A3FF. And incidentally, 1 more than each of these is 0xAAAA0001 and 0x0000A400.

The biggest problem with pointers is the same problem incurred by house addresses. You need to think about the number of times you’ve received your neighbor’s mail (and vice versa). Likewise, applications can have invalid pointers, and when the code tries to process this invalid address, it often crashes the application. Of course, the worst problem is the null pointer, `0x00000000`, which you expect to point to something. A null pointer points to nothing.

Another problem with pointers is that you spend a lot of time managing them, and who can remember all that code! Every time you work with pointers, you risk:

- **Creating a memory leak:** By not deallocating the pointer so you can reuse the memory, the memory becomes inaccessible to the application. You could actually run out of memory despite having memory available. The memory becomes available again after the operating system frees it once the application terminates.
- **Using memory that hasn’t been initialized:** The memory location could contain anything and if you act on the data in that memory location, your application will act oddly or simply crash.
- **Obtaining the wrong data:** The application could point to the wrong location and you might not know it. This means that the application is using the wrong data, which could result in unanticipated output or data damage.

## Writing cleaner and less bug-prone code

To write cleaner code with fewer bugs, you need to find a way to get the effects of a pointer without any of the disadvantages of pointers. The C++ committee has been working on this issue. For example, `std::auto_ptr` is deprecated (set for deletion, but still allowed) in C++11 and removed in C++17. Here are some modern ways of getting past pointers:

- **Using smart pointers:** Boost (explained in Book 7, Chapter 4) has provided access to smart pointers for a long time, and many developers use them because they make both dynamic allocation and runtime polymorphism easier to deal with. Using a smart pointer, such as `std::unique_ptr` or `std::shared_ptr`, eliminates the need for you to manage memory manually. Instead, the smart pointer addresses memory management needs for you so that you can concentrate on writing business logic rather than performing low-level programming tasks.
- **Relying on optional pointers:** C++17 introduced `std::optional` as the means for working with nullable references. When an optional pointer is null, it has a value of `std::nullopt`, which is actually an important thing to know when dealing with them. The only problem is that the implementation is flawed because it lacked support for references (pointers to pointers) and had no monadic (entity operator) interface (see http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2017/p0798r0.html for a discussion of this extremely advanced concept not covered in this book). The short version is that it didn’t do what raw pointers could do, but these problems are fixed in C++20.
- **Passing objects around:** A modern computer isn’t nearly as resource limited as those in the past were, so modern languages commonly pass objects around rather than create pointers to them. This solution addresses the need to eliminate unwanted copies. C++20 provides two solutions for this task, both of which rely on the idea of using the object `obj`, which is outside the function, to directly construct the object being initialized inside the function and that is returned from it.

You can view this optimization as: `T obj = f();`, where `f()` is a function that initializes `obj` of type `T`. Here is how the optimizations differ:

- **Return Value Optimization (RVO):** In this case, you could have a function that looks like this:

```
T f() {
    ... // Do something here.
    return T(constructor arguments);
}
```

In this case, you could create three objects of type T: the unnamed temporary object created by the return statement; the temporary object returned by `f()` to the caller; and the named object, `obj`, copied from the return from `f()`. Using RVO eliminates the two temporary objects by initializing `obj` directly with the arguments passed inside the body of `f()`. This is actually a complex topic that's outside the purview of this book, but you can read a discussion of the details of this topic at `https://shahmike.com/cpp/rvo/`.

![](img/128ab511de4e7360e167e3b15cdd5dd0_211_1.png)

- **Named Return Value Optimization (NRVO):** This form of optimization goes a step further than RVO when the return statement uses a named value, as shown here:

```
T f() {
    ... // Do something here.
    T result(constructor arguments);
    return result;
}
```

This technique effectively replaces the hidden object and the named object inside the function with the object used for holding the result. The only caveat is that result must be unique so that the compiler knows which object inside `f()` to use to construct the memory in `obj`. NRVO is a particular kind of copy elision (the process of joining together or merging of objects) discussed in detail at `https://en.cppreference.com/w/cpp/language/copy_elision`.

## Referring to Your Data Through Pointers

![](img/128ab511de4e7360e167e3b15cdd5dd0_211_0.png)

### Heaping and Stacking the Variables

C++ applications use two kinds of memory:

- **Heap:** A common area in memory where you can store global variables. This is where you also store objects and variables that you allocate from memory.
