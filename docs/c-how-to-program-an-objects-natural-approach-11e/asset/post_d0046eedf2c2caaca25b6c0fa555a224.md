
## 19.6.12 Setting and Resetting the Format State via Member Function Flags

You’ve seen how to use stream manipulators to change output format characteristics, but how do you return an output stream’s format to its previous state after changing its format? Member function `flags` without an argument returns the current format state settings as a `fmtflags` object. Member function `flags` with a `fmtflags` argument sets the format state as specified by the argument and returns the prior state settings. The initial settings of the value that `flags` returns might vary among compilers. Figure 19.18 uses member function `flags` to save the stream’s original format state (line 16), then restore the original format settings (line 24). The capabilities for capturing the format state and restoring it are not required in C++20 text formatting. Each `std::format` call’s formatting is used only in that call and does not affect any other `std::format` call, thus simplifying output formatting.

```cpp
// fig19_18.cpp
// flags member function.
#include <format>
#include <iostream>

int main() {
   int integerValue{1000};
   double doubleValue{0.0947628};

   // display flags value, int and double values (original format)
   std::cout << std::format("flags value: {}\n", std::cout.flags())
      << "int and double in original format:\n"
      << integerValue << '\t' << doubleValue << "\n\n";

   // save original format, then change the format
   auto originalFormat{std::cout.flags()};
   std::cout << std::showbase << std::oct << std::scientific;

   // display flags value, int and double values (new format)
   std::cout << std::format("flags value: {}\n", std::cout.flags())
      << "int and double in new format:\n"
      << integerValue << '\t' << doubleValue << "\n\n";

   std::cout.flags(originalFormat); // restore format

   // display flags value, int and double values (original format)
   std::cout << std::format("flags value: {}\n", std::cout.flags())
      << "int and double in original format:\n"
      << integerValue << '\t' << doubleValue << "\n";
}
```

**Fig. 19.18** | flags member function. (Part 1 of 2.)

```text
flags value: 513
int and double in original format:
1000    0.0947628

flags value: 5129
int and double in new format:
01750    9.476280e-02

flags value: 513
int and double in original format:
1000    0.0947628
```

**Fig. 19.18** | flags member function. (Part 2 of 2.)

## 19.7 Stream Error States

Each stream object contains a set of state bits representing the stream’s state—sticky format settings, error indicators, etc. You can use this information to test, for example, whether an input was successful. These state bits are defined in class `ios_base`—the base class of the stream classes. Stream extraction sets the stream’s `failbit` to true if the wrong type of data is input. Similarly, stream extraction sets the stream’s `badbit` to true if the operation fails in an unrecoverable manner—for example, if a disk fails when a program is reading a file from that disk. Figure 19.19 shows how to use bits like `failbit` and `badbit` to determine a stream’s state.⁴ See the Bit Manipulation appendix at https://deitel.com/cpphtp11 for more information on bits and bit manipulation.

```cpp
// fig19_19.cpp
// Testing error states.
#include <iostream>

int main() {
   int integerValue{0};

   // display results of cin functions
   std::cout << std::boolalpha << "Before a bad input operation:"
      << "\n  cin.rdstate(): " << std::cin.rdstate()
      << "\n  cin.eof(): " << std::cin.eof()
      << "\n  cin.fail(): " << std::cin.fail()
      << "\n  cin.bad(): " << std::cin.bad()
      << "\n  cin.good(): " << std::cin.good()
      << "\n\n expects an integer, but enter a character: ";

   std::cin >> integerValue; // enter character value
```

**Fig. 19.19** | Testing error states. (Part 1 of 2.)

```cpp
   // display results of cin functions after bad input
   std::cout << "\nAfter a bad input operation:"
             << "\n  cin.rdstate(): " << std::cin.rdstate()
             << "\n  cin.eof(): " << std::cin.eof()
             << "\n  cin.fail(): " << std::cin.fail()
             << "\n  cin.bad(): " << std::cin.bad()
             << "\n  cin.good(): " << std::cin.good();

   std::cin.clear(); // clear stream

   // display results of cin functions after clearing cin
   std::cout << "\nAfter cin.clear()"
             << "\n  cin.fail(): " << std::cin.fail()
             << "\n  cin.good(): " << std::cin.good() << "\n";
}
```

```text
Before a bad input operation:
  cin.rdstate(): 0
  cin.eof(): false
  cin.fail(): false
  cin.bad(): false
  cin.good(): true

 expects an integer, but enter a character: A

After a bad input operation:
  cin.rdstate(): 2
  cin.eof(): false
  cin.fail(): true
  cin.bad(): false
  cin.good(): false

After cin.clear()
  cin.fail(): false
  cin.good(): true
```

**Fig. 19.19** | Testing error states. (Part 2 of 2.)

### Member Function eof

The program begins by displaying the stream’s state before receiving any input from the user (lines 9–14). Line 11 uses member function `eof` to determine whether the end-of-file has been encountered on the stream. In this case, the function returns 0 (false). The function checks the value of the stream’s `eofbit` data member, which is set to true for an input stream after the end-of-file is encountered after an attempt to extract data beyond the end of the stream.

### Member Function fail

Line 12 uses the `fail` member function to determine whether a stream operation has failed. The function checks the value of the stream’s `failbit` data member, which is set to true on a stream when a format error occurs and, as a result, no characters are input. For example, this might occur when you attempt to read a number, but the user enters a string. In this case, the function returns 0 (false). When such an error occurs on input, the characters are not lost. Usually, recovering from such input errors is possible.

### Member Function bad

Line 13 uses the `bad` member function to determine whether a stream operation failed. The function checks the value of the stream’s `badbit` data member, which is set to true for a stream when an error occurs that results in the loss of data—such as reading from a file when the disk on which the file is stored fails. In this case, the function returns 0 (false). Generally, such serious failures are nonrecoverable.

### Member Function good

Line 14 uses the `good` member function, which returns true if the `bad`, `fail` and `eof` functions would all return false. The function checks the stream’s `goodbit`, which is set to true for a stream if none of the bits `eofbit`, `failbit` or `badbit` is set to true for the stream. In this case, the function returns 1 (true). I/O operations should be performed only on “good” streams.

### Member Function rdstate

The `rdstate` member function (line 10) returns the stream’s overall error state as an integer value. The function’s return value could be tested, for example, by a `switch` statement that examines `eofbit`, `badbit`, `failbit` and `goodbit`. The preferred means of testing the state of a stream is to use member functions `eof`, `bad`, `fail` and `good`—using these functions does not require you to be familiar with particular status bits.

### Causing an Error in the Input Stream and Redisplaying the Stream’s State

Line 17 reads a value into an `int` variable. Enter a string rather than an `int` to force an error to occur in the input stream. At this point, the input fails, and lines 20–25 once again call the stream’s state functions. In this case, `fail` returns 1 (true) because the input failed. Function `rdstate` also returns a nonzero value (true) because at least one of the member functions `eof`, `bad` and `fail` returned true. Once an error occurs in the stream, function `good` returns 0 (false).

### Clearing the Error State, So You May Continue Using the Stream

After an error occurs, you can no longer use the stream until you reset its error state. The `clear` member function (line 27) is used to restore a stream’s state to “good,” so that I/O may proceed on that stream. Lines 30–32 show that `fail` returns 0 (false) and `good` returns 1 (true), so the input stream can be used again.

The default argument for `clear` is `goodbit`, so the statement

```cpp
std::cin.clear();
```

clears `cin` and sets `goodbit` for the stream. The statement

```cpp
std::cin.clear(ios::failbit)
```

sets the `failbit`. You might want to do this when performing input on `cin` with a user-defined type and encountering a problem. The name `clear` might seem inappropriate in this context, but it’s correct.

⁴ The actual values output by this program may vary among compilers.
