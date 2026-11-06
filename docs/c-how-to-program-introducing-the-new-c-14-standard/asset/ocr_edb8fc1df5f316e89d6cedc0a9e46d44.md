# 13.4.1 `get` and `getline` Member Functions

The `get` member function with *no arguments* inputs *one character* from the designated stream (including white-space characters and other nongraphic characters, such as the key sequence that represents end-of-file) and returns it as the value of the function call. This version of `get` returns `EOF` when *end-of-file* is encountered on the stream. `EOF` normally has the value `-1` and is defined in a header that’s indirectly included in your code via stream library headers like `<iostream>`.

# *Using Member Functions `eof`, `get` and `put`*

**Figure 13.2** demonstrates member functions `eof` and `get` on input stream `cin` and member function `put` on output stream `cout`. This program uses `get` to read characters into the `int` variable `character`, so that we can test each character entered to see if it’s `EOF`. We use int because on many platforms `char` can represent only nonnegative values and `EOF` is typically `-1`. The program first prints the value of `cin.eof()`—i.e., `false` (`0` on the output)—to show that *end-of-file* has