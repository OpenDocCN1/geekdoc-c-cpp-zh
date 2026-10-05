
changed << val methods.

```
// https://godbolt.org/z1xzzMjdjM
#include <iostream>
using std::cout; using std::endl;
int main() {
    int val = 255;
    cout.setf(std::ios_base::hex, std::ios_base::basefield);
    cout.setf(std::ios_base::showcase);
    cout << val << std::endl; // Output: 0xff
    cout.unsetf(std::ios_base::showcase);
    cout.setf(std::ios_base::dec, std::ios_base::basefield);
    cout << val << std::endl; // Output: 255
}
```

# Listing 27.13 Influencing format with "setf" and "unset"

Here the same thing happens as in Listing 27.12.

I think the example shows the clearer and more convenient use of manipulators as opposed to the methods setf() and unsetf() used here. With manipulators, you don't have to deal with cumbersome things like flags, bits, and bitmasks. And ultimately, a manipulator like std::showbase internally calls the cout.setf(std::ios::showbase) method anyway.

Some format of the flags can also be used in groups, as seen in the example of dec with basefield. Specifically, there are three groups with adjustfield (and the flags left, right, internal), basefield (with the flags dec, oct, hex), and floatfield (with the flags scientific and fixed).

Independent flags, such as showcase, can be used alone with ios_base:: or ios::. Table 27.7 provides an view of the methods in the ios_base class, which allow you to directly change the format flags.

| Method | Meaning |
| --- | --- |
| setf(flags) | Sets the format flags to flags. |
| setf(flags, group) | Sets the format flags of the group to flags. |
| unsetf(flags) | Clears all flags. |
| flags() | Returns the currently set format flags. |
| flags(flags) | Sets the format flags to flags. |

Table 27.7 Methods for accessing format flags.

The next listing is the same as the previous one, but now everything should be implemented using only the flags() method.

```
// https://godbolt.org/z/4MY1Zznv9
#include <iostream>
using std::cout; using std::endl;
int main() {
    int val = 255;
    std::ios::iflags ff = std::cout.flags();
    cout.flags(std::ios::hex | std::ios::showbase);
    cout << val << endl; // Output: 0xff
    cout.flags(ff);
    cout << val << endl; // Output: 255
}
```

# Listing 27.14 Saving and restoring flags.

I retrieve the current state of the format flags with flags() and store it in ff. Calling flags(...) with the hex and showcase parameters for the cout stream changes the format. Afterward, I restore the previously saved state of the format flags, which the output at the end confirms.

# Further Methods for Formatting

You will also find suitable methods in the ios_base class (see Table 27.8) for some manipulators with parameters, primarily to format variable output (like precision or fill width).

| Method | Description |
| --- | --- |
| int fill() const | Returns the currently set fill character. |
| int fill(int ch) | Sets the fill character to ch. Equivalent to << setfill(ch). |
| int width() const | Returns the field width. |
| int width(int n) | Sets the field width to n. Equivalent to << setw(n). |
| int precision() const | The current precision of floating-point numbers. |

| Method | Description |
| :--- | :--- |
| int precision(int n) | Sets the precision to n. Equivalent to << setprecision(n). |

# width() Is Different

As with the manipulator setw(), the fill width setting using width() does not remain permanent, unlike all other flags. The fill width is reset after each use and must therefore be set again before each use.

# 27.6 Streams for File Input and Output

You've been using the computer for a while now, and you've found yourself working with variables in the system's memory. You've probably noticed that when you close the program, all those variables just disappear. Well, don't worry, because in this section, I am going to show you you can save those variables permanently on an external storage device so that you can access them whenever you need them.

Before we get started, I just want to quickly go over how you can access files. To access files, you'll need certain functions. These are provided by the C++ standard library. When reading and writing files, you don't access them byte by byte. Instead, you access them in larger blocks to improve efficiency. For this kind of data transfer, we use a buffer as a temporary storage space in the RAM. You can think of the file or the file's contents as an array of bytes with a specific length.

And just like you write the data into a file, you can also read it out again. So, you'll need to take care of the.

## 27.6.1 The "ifstream", "ofstream", and "fstream" Streams

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

## 27.6.2 Connecting to a File

To do anything with a file, you must first instantiate a stream object of type ifstream, ofstream, or fstream. Then open the file with a stream object of type ifstream, ofstream, or fstream.

## 27.6.3 No Path Specified.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

The standard classes for file input and output are:
- ifstream: for reading files.
- ofstream: for writing to files.
- fstream: for both reading and writing files.

# Listing 27.15 Opening and creating files.

```cpp
// https://godbolt.org/z/o7YPor8s
#include <fstream>
#include <iostream>
#include <string>
int main() {
    std::string name = "text.txt";
    std::ifstream file01;
    file01.open(name);
    if (file01.fail()) {
        std::cout << "Could not open " << name << "\n";
    }
    std::ofstream file02("data.dat");
    if (file02.good()) {
        std::cout << "data.dat opened or created\n";
    }
    std::ifstream file03;
    file03.open("database.db");
    if (!file03) {
        std::cout << "Could not open database.db\n";
    }
}
```

# Error Checking

For error checking when opening a file, you can use both if(!file) and if(file.fail()). In both cases, true will be returned if opening a file has failed and thus the failbit flag is set (see also Section 27.4). If a file is successfully opened, all error flags are cleared, and the goodbit flag is set.
