
A string_view does not update automatically if the contents it views change in size after you initialize the string_view.

string_views enable many string-style operations on C-strings without the overhead of creating and initializing string objects, which copies the C-string contents. The C++ Core Guidelines state that you should prefer string objects if you need to “own character sequences”—for example, so you can modify a string’s contents.² If you need a read-only view of a contiguous sequence of characters, the C++ Core Guidelines recommend using a string_view.³

### Creating a string_view

Figure 8.9 demonstrates several string_view features. We broke this example into parts for discussion. Line 6 includes the header `<string_view>`. Line 9 creates the string s1, and line 10 copies s1 into the string s2. Line 11 uses s1 to initialize a string_view.

```cpp
// fig08_09.cpp
// Demonstrating string_view.
#include <format>
#include <iostream>
#include <string>
#include <string_view>

int main() {
   std::string s1{"red"};
   std::string s2{s1};
   std::string_view v1{s1}; // v1 “sees” the contents of s1
   std::cout << std::format("s1: {}\ns2: {}\nv1: {}\n", s1, s2, v1);
}
```

```text
s1: red
s2: red
v1: red
```

**Fig. 8.9** | Demonstrating string_view.

### string_views “See” Changes to the Characters They View

A string_view does not own the sequence of characters it views but “sees” any changes to the original characters. Line 15 modifies the std::string s1. Then line 16 shows s1’s, s2’s and the string_view v1’s contents. Note that s2 was not modified because it owns a copy of s1’s contents.

```cpp
// string_views see changes to the characters they view
s1.at(0) = 'R'; // capitalize s1
std::cout << std::format("s1: {}\ns2: {}\nv1: {}\n\n", s1, s2, v1);
```

```text
s1: Red
s2: red
v1: Red
```

### string_views Can Be Compared to std::strings or string_views

Like strings, string_views support the relational and equality operators. You also can intermix std::strings and string_views as in line 20’s == comparisons.

```cpp
// string_views are comparable with strings or string_views
std::cout << std::format("s1 == v1: {}\ns2 == v1: {}\n\n",
    s1 == v1, s2 == v1);
```

```text
s1 == v1: true
s2 == v1: false
```

### string_views Can Remove a Prefix or Suffix

You can easily remove a specified number of characters from the beginning or end of a string_view. These are fast operations for a string_view. They adjust the character count and, if necessary, move the pointer to string_view’s first remaining character. Lines 23–24 call string_view member functions remove_prefix and remove_suffix to remove one character from the beginning and one from the end of v1, respectively. Note that s1 remains unmodified.

Perf

```cpp
// string_view can remove a prefix or suffix
v1.remove_prefix(1); // remove one character from the front
v1.remove_suffix(1); // remove one character from the back
std::cout << std::format("s1: {}\nv1: {}\n\n", s1, v1);
```

```text
s1: Red
v1: e
```

### string_views Are Iterable

Line 28 initializes a string_view from a C-string. Like strings, string_views are iterable, so you can use them with the range-based for statement, as in lines 30–32.

```cpp
// string_views are iterable
std::string_view v2{"C-string"};
std::cout << "The characters in v2 are: ";
for (char c : v2) {
    std::cout << c << " ";
}
```

```text
The characters in v2 are: C - s t r i n g
```

### string_view Enables Various String Operations on C-Strings

Many string member functions that do not modify a string’s contents also are defined for string_views. For example,

- line 35 calls `size` to determine how many characters the `string_view` can “see,”
- line 36 calls `find` to get the index of `'-'` in the `string_view` and
- lines 37–38 use the new C++20 `starts_with` function to determine whether the `string_view` starts with `'C'`.

```cpp
34    // string_view enables various string operations on C-Strings
35    std::cout << std::format("\nv2.size(): {}\n", v2.size());
36    std::cout << std::format("v2.find('-'): {}\n", v2.find('-'));
37    std::cout << std::format("v2.starts_with('C'): {}\n",
38        v2.starts_with('C'));
39 }
```

```text
v2.size(): 8
v2.find('-'): 1
v2.starts_with('C'): true
```

### ✓ Checkpoint

- 1. **(True/False)** Like a span, a string_view owns the data it views.  
  **Answer:** False. Actually, neither owns the data it views.
- 2. **(True/False)** It is costly to remove characters from a string_view’s beginning or end.  
  **Answer:** False. Actually, removing a specified number of characters from a string_view’s beginning or end is fast. These operations adjust the character count and, if necessary, move the pointer to the string_view’s first remaining character.
- 3. **(Fill-in)** Like strings, string_views are __________, so you can use them with the range-based for statement.  
  **Answer:** iterable.

## 8.12 Files and Streams

C++ views each file simply as a sequence of bytes:

![](img/7b5e2088e71c7f78681d4ddbcf104c06_435_0.png)

Each file ends either with an end-of-file marker or at a specific byte number recorded in an operating-system-maintained administrative data structure. When a file is opened, an object is created, and a stream is associated with the object. The objects cin, cout, cerr and clog are created for the header `<iostream>`. The streams associated with these objects provide communication channels between a program and a particular file or device. The `cin` object (standard input stream object) enables a program to input data from the keyboard or other devices. The `cout` object (standard output stream object) enables a program to output data to the screen or other devices. The `cerr` and `clog` standard error stream objects enable a program to output error messages to the screen or other devices. Messages written to `cerr` are output immediately. In contrast, messages written to `clog` are stored in a memory object called a buffer. When the buffer is full, its contents are written to the standard error stream.

### File-Processing Streams

File processing requires header `<fstream>`, which includes the following definitions:

- `ifstream` is for file input.
- `ofstream` is for file output.
- `fstream` combines the capabilities of `ifstream` and `ofstream`.

The `cout` and `cin` capabilities we’ve discussed so far and the additional I/O features we describe in Chapter 19 also can be applied to file streams.

### Checkpoint

- 1. **(Fill-in)** C++ views each file simply as ________.  
  **Answer:** a sequence of bytes.
- 2. **(Fill-in)** Each file ends either with a(n) ________ or at a specific byte number recorded in an operating-system-maintained administrative data structure.  
  **Answer:** end-of-file marker.
- 3. **(Fill-in)** Messages written to `cerr` are output immediately, whereas messages written to `clog` are stored in a memory object called a ________. When this object is full (or flushed), its contents are written to the standard error stream.  
  **Answer:** buffer.

## 8.13 Creating a Sequential File

C++ imposes no structure on files. Thus, a concept like that of a record containing related data items does not exist. You structure files to meet your application’s requirements. The following example shows how to impose a simple record structure on a file.

Figure 8.10 creates a sequential file that might be used in an accounts-receivable system to help keep track of the money owed to a company by its credit clients. For each client, the program obtains the client’s account number, name and balance (i.e., the amount the client owes the company for goods and services received in the past). The data obtained for each client constitutes a record for that client.

```cpp
// fig08_10.cpp
// Creating a sequential file.
#include <cstdlib> // exit function prototype
#include <format>
#include <fstream> // contains file stream processing types
#include <iostream>
#include <string>

int main() {
   // ofstream opens the file
   if (std::ofstream output{"clients.txt", std::ios::out}) {
      std::cout << "Enter the account, name, and balance.\n"
                << "Enter end-of-file to end input.\n\n";

      int account;
      std::string name;
      double balance;

      // read account, name and balance from cin, then place in file
      while (std::cin >> account >> name >> balance) {
         output << std::format("{} {} {}\n", account, name, balance);
         std::cout << "? ";
      }
   }
   else {
      std::cerr << "File could not be opened\n";
      std::exit(EXIT_FAILURE);
   }
}
```

```text
Enter the account, name, and balance.
Enter end-of-file to end input.
? 100 Dey 24.98
? 200 Taylor 345.67
? 300 Huber 0.00
? 400 Karimov -42.16
? 500 Sosa 224.62
? ^Z
```

**Fig. 8.10** | Creating a sequential file.

### Opening a File

Figure 8.10 writes data to a file, so we open the file for output by creating an ofstream object (line 11) and initializing it with the filename and the file-open mode. The file-open mode is `ios::out`, the default for an ofstream object, so the second argument in line 11 is not required. Use caution when opening an existing file for output (`ios::out`). Existing files opened in mode `ios::out` are truncated—all data in the file is discarded without warning. If the file does not exist, the ofstream object creates the file.

Line 11 creates the ofstream object `output` associated with the file `clients.txt` and opens it for output. We did not specify a path to the file on disk, so it’s placed in the same folder as the program’s executable file. In legacy C++ code, the filename was specified as a pointer-based string. Modern C++ allows you to specify the filename as a string object.
