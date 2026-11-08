
The while loop comes from the classic Unix framework, which simply reads all characters from the `cin` stream unformatted and outputs them to the `cout` stream. Reading continues until a period is entered or EOF is reached.

The program during execution looks like this:

```text
Input getline: Hello getline
9 characters were read
Hello get
Make an input (end with .): Hello get
Hello get
Another line
Another line
We end with a period.
We end with a period
Input ended
```

> **`std::string` and `getline()`**
>
> In the `<string>` header file, you will also find a `getline()` method that reads a line from a stream into a `std::string`.

## 27.4 Error Handling and Stream States

For streams, it is often not enough to simply check whether something works (`true`) or does not work (`false`). Because various types of errors can occur, the I/O stream library provides mechanisms to check the state of the stream. For this, you will find a few constants with `iostate` from `ios_base` (see Table 27.1).

The constants are defined in `ios_base` as public members and can be accessed either directly via `ios_base` (e.g., `ios_base::goodbit`) or through classes derived from `ios_base` or created objects (e.g., `ios::goodbit` or `cout.goodbit`).

| Constant | Meaning |
| --- | --- |
| `goodbit` | No problems with the stream. All other bits are not set. |
| `eofbit` | EOF is set. The end of a data stream has been reached. |
| `failbit` | Error in an input/output function. An input/output operation could not be successfully executed. |
| `badbit` | Severe error. The stream is in an undefined state. |

**Table 27.1** Constants in `iostate`.

### 27.4.1 Methods for Handling Stream Errors

To query the individual states, C++ offers you various methods:

- `bool good()`  
  Returns true if everything is okay (`goodbit` is set).
- `bool eof()`  
  Returns true if the file stream has ended (`eofbit` is set).
- `bool fail()`  
  Returns true if an error has occurred (`failbit` or `badbit` are set).
- `bool bad()`  
  Returns true if a serious error has occurred (`badbit` is set).
- `void clear()`  
  Resets the state of `iostate`. Status is set to `goodbit`.
- `void clear(iostate f)`  
  Resets the state of `iostate` and sets the status to `f`.
- `void setstate(iostate f)`  
  The current state is combined with `f` using a bitwise OR.
- `iostate rdstate()`  
  Returns the currently set status.

> **`eofbit` and `failbit` Set**
>
> Usually, `failbit` is also set when `eofbit` is set. The reason is that the `eofbit` state is only set after an attempt is made to perform another action past the EOF. This also means that the next operation fails, and therefore `failbit` is set as well.

```cpp
// https://godbolt.org/z/exKMv8646
#include <fstream>
#include <iostream>
using std::cout; using std::cin; using std::ofstream;
void checkIOState(std::ios& stream) {
    if( stream.good() ) {
        cout << "All good\n";
    } else if( stream.bad() ) {
        cout << "Fatal error\n";
    } else if( stream.fail() ) {
        cout << "I/O error\n";
        if( stream.eof() ) {
            cout << "End of stream reached\n";
        }
    }
    stream.clear();
}
int main() {
    int val=0;
    cout << "Enter value: ";
    cin >> val;
    checkIOState( cin );
    std::ifstream file;
    file.open("nonexistent.text");
    checkIOState(file);
    std::fstream fstr;
    fstr.open("newFile.txt",
        ofstream::out | ofstream::binary | ofstream::trunc);
    fstr << "Text in the file\n";
    fstr.seekp(std::ios_base::beg);
    char ch;
    while( fstr.good()) {
        fstr.get(ch);
        if(fstr.good()) cout.put(ch);
    }
    checkIOState(fstr);
}
```

**Listing 27.3** State checks for streams.

Pass any stream to the `checkIOState()` function to check its state. I check the individual methods to clarify the state. At the end, I reset the state with `clear()` back to `goodbit`.

In the section starting from `val=0`, you will be prompted to enter a value. Correctly, you must enter an integer here. With `checkIOState`, I then check the `cin` stream. If the input is correct, `goodbit` is set, and `good()` is true. For an incorrect input like `blablubb`, `fail()` is true.

For the `ifstream` file, I check a file stream `std::ifstream`, because with it I can open a file for reading. In the example, it is assumed that the file does not exist, which is why `fail()` is true here as well.

And finally, starting from `fstream` fstr, I demonstrate EOF. Between open and seekp, I create a file, write something into it, and reset the data stream to the beginning. In the while loop, I read characters from the fstr stream as long as the state of fstr is equal to `good()` (`goodbit` set). If the state is no longer `good()`, either the end of the data stream has been reached (`eofbit` is set) or an error has occurred (`failbit` is set). As already mentioned, `failbit` is usually also set when `eofbit` is set.

> **Exception `ios_base::failure`**
>
> In case of errors in the I/O stream library, the `ios_base::failure` exception can also be thrown (if `badbit` is set). However, this depends on the implementation of the compiler manufacturer. Nevertheless, it is possible to throw and catch this exception yourself using `throw`.

### Checking Streams with “bool”

The state of the stream can also be tested with `bool` and the `!` operator. Both have been implemented as methods in `ios_base` (`operator bool()` and `operator!()`). Both methods return whether an error has occurred (`failbit` or `badbit` set).

For example, the `operator bool()` is used as shown in the next listing.

```cpp
// https://godbolt.org/z/Mr6E3Ez48
#include <iostream>
int main() {
    unsigned int val;
    std::cout << "Enter value: ";
    std::cin >> val;
    if( std::cin ) { //operator bool()
        /*...*/                      // Input correct
    } else {
        std::cout << "Error with std::cin\n";  // Error with input
    }
}
```

**Listing 27.4** Operator “bool” of streams.

In `if( std::cin )...`, the stream, because it is used in an `if`, is automatically converted to `bool`. The `operator bool()` is defined in the class specifically for such purposes. You can just as easily apply the `!` operator to streams.

## 27.5 Manipulating and Formatting Streams

How characters are input or output in a stream is controlled by so-called flags, which are defined in the `ios_base` class. You can think of flags as an array of bits, where the values can be either 1 or 0. Individual bits, of course, do not make a value, so the bits are stored in a variable. Depending on the set bits, the value of the variable changes, and each value has a special meaning. All flags have a default setting, where, for example, without further specification, all integral values are output in decimal (`dec`) notation.

You can directly change the format flags by using methods like `setf()`, `unsetf()`, or `flags()` from the `ios_base` class. However, a better alternative has been available for a long time (specifically) with manipulators. With these, you can insert and call all flags directly as a function in an input or output stream. In practice, the use of manipulators is therefore usually preferable to direct access to the format flags with methods. Therefore, manipulators will be discussed first. The methods by which you can directly change the format flags will be briefly introduced in Section 27.5.4.

### 27.5.1 Manipulators

Manipulators for streams are objects that you can insert with the standard input/output operators `<<` and `>>`. You are already familiar with the manipulator `endl`. This adds a newline character to the buffer to output a new line. The basic manipulators are listed in `<istream>` and `<ostream>` in Table 27.2.

| Manipulator | Meaning |
|---|---|
| `endl` | Outputs a new line and flushes the output buffer. |
| `ends` | Adds the null terminator character (`'\0'`) to the buffer. |
| `flush` | Flushes the stream's output buffer. |
| `ws` | Ignores leading whitespace when reading input. |

**Table 27.2** Basic manipulators in `<istream>` and `<ostream>`.

### Independent Manipulators in `<ios>`

You can find a considerable number of additional manipulators in the header file `<ios>`. These are manipulators to enable or disable certain states or to format the data during output. I summarized the manipulators in Chapter 6, Table 6.3.

Since C++20, you can often use `format()` instead of the manipulators. This allows you to convert built-in and custom types into a string. You can find the description in Section 27.10.

It is easy to enable or disable states. Once (de)activated in a particular stream, the state remains until you call the opposite manipulator again. Consider the following simple example.

```cpp
// https://godbolt.org/z/s1csa51z9
#include <iostream>
#include <iomanip>
using std::cin; using std::cout; using std::endl;
void f(bool b) {
    cout << b << endl;                         // Output: true
}
```
