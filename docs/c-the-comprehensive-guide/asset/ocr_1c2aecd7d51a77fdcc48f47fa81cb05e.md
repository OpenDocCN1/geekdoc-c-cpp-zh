You can also sometimes use `string_view` as a return value. However, just as with pointers and references, you must ensure that the original string on which the `string_view` is based still exists.

# ## 6.2 Streams

You have seen streams in examples many times, but rarely did their type appear because we used the predefined streams of the standard library:

+   - `std::cout` of type `std::ostream` is used for *standard output*, usually to the console—that is, the screen. Or you can redirect the output to a file.
+   - `std::cin` of type `std::istream` is used for *standard input*, usually from the keyboard or a redirected file.
+   - `std::cerr` and `std::clog` are also output data streams of type `std::ostream` and usually end up on the screen, but you can redirect them to a file separately from `std::cout`.

For inputs and outputs of a normal program flow, you normally use `std::cin` and `std::cout`. Each output takes time, and a call has overhead, so `std::cout` is buffered: outputs sometimes do not appear immediately, but are collected first.

Not so with `std::cerr`, whose output should appear immediately. Use this stream for error output. If `std::cout` has been redirected to a file, this output will still appear on the console, as shown in [Listing 6.3](#listing-63).

```
```cpp
// https://godbolt.org/z/P1fn5q8z8
// Call this program with "prog.exe > file.txt", for example.
#include <iostream>  // cout, cerr
int main() {
    std::cout << "Output to cout\n";       // is output after file.txt
    std::cerr << "Error message!\n";       // still appears on the console
    std::cout << "Normal output again\n";  // back into the file
}
```
```

**Listing 6.3** The error stream is separated from the standard output.

# ### 6.2.1 Input and Output Operators

As you have often seen, you can use the `<<` operator to output data to `cout`. All built-in data types can be output in this way. You do not have to worry about the format—but you can do so, as you will see in a moment with the *manipulators*. This is worth mentioning because, unlike in the C function `printf()`, the compiler selects the correct format for you—namely, the correct overload of the global `operator<<`. You can also add overloads for your own data types (see Chapter 12, Section 12.11).