
## TRY THIS

- Make a simple table including the last name, first name, telephone number, and email address for yourself and at least five of your friends. Experiment with different field widths until you are satisfied that the table is well presented.

## 11.3 File opening and positioning

As seen from C++, a file is an abstraction of what the operating system provides. As described in §10.3, a file is simply a sequence of bytes numbered from 0 upward:

```
0: 1: 2:
[  ][  ][  ][  ][  ][  ][  ][  ][  ][  ][  ][  ]
```

The question is how we access those bytes. Using **iostreams**, this is largely determined when we open a file and associate a stream with it. The properties of a stream determine what operations we can perform after opening the file, and their meaning. The simplest example of this is that if we open an **istream** for a file, we can read from the file, whereas if we open a file with an **ostream**, we can write to it.

### 11.3.1 File open modes

You can open a file in one of several modes. By default, an **ifstream** opens its file for reading and an **ofstream** opens its file for writing. That takes care of most common needs. However, you can choose between several alternatives:

| File stream open modes | Description |
| :--- | :--- |
| `ios_base::app` | append (i.e., add to the end of the file) |
| `ios_base::ate` | "at end" (open and seek to end) |
| `ios_base::binary` | binary mode — beware of system-specific behavior |
| `ios_base::in` | for reading |
| `ios_base::out` | for writing |
| `ios_base::trunc` | truncate file to 0 length |

A file mode is optionally specified after the name of the file. For example:

```cpp
ostream of1 {name1};              // defaults to ios_base::out
istream if1 {name2};               // defaults to ios_base::in

ostream ofs {name, ios_base::app}; // ofstreams by default include
                                   // ios_base::out
fstream fs {"myfile", ios_base::in|ios_base::out};   // both in and out
```

The `|` in that last example is the “bitwise or” operator (§A.5) that can be used to combine modes as shown. The `app` option is popular for writing log files where you always add to the end.

In each case, the exact effect of opening a file may depend on the operating system, and if an operating system cannot honor a request to open a file in a certain way, the result will be a stream that is not in the `good()` state:

```cpp
if (!fs)          // oops: we couldn’t open that file that way
```

The most common reason for a failure to open a file for reading is that the file doesn’t exist (at least not with the name we used):

```cpp
ifstream ifs {"readings"};
if (!ifs)         // error: can’t open “readings” for reading
```

In this case, we guess that a spelling error might be the problem.

Note that typically, an operating system will create a new file if you try to open a nonexistent file for output, but (fortunately) not if you try to open a nonexistent file for input:

```cpp
ostream ofs {"no-such-file"};            // create new file called no-such-file
ifstream ifs {"no-file-of-this-name"};    // error: ifs will not be good()
```

Try not to be clever with file open modes. Operating systems don't handle "unusual" mode consistently. When you can, stick to reading from files opened as **istreams** and writing to files opened as **ostreams**.

### 11.3.2 Binary files

In memory, we can represent the number 123 as an integer value or as a string value. For example:

```cpp
int n = 123;
string s = "123";
```

In the first case, **123** is stored as a (binary) number in an amount of memory that is the same as for all other **ints** (4 bytes, that is, 32 bits, on a PC). Had we chosen the value **12345** instead, the same 4 bytes would have been used. In the second case, **123** is stored as a string of three characters. Had we chosen the string value "**12345**" it would have used five characters (plus the fixed overhead for managing a **string**). We could illustrate this like this (using the ordinary decimal and character representation, rather than the binary representation actually used within the computer):

```
123 as characters: | 1 | 2 | 3 | ? | ? | ? | ? | ? |
12345 as characters: | 1 | 2 | 3 | 4 | 5 | ? | ? | ? |
123 as binary: | 123 |
12345 as binary: | 12345 |
```

When we use a character representation, we must use some character to represent the end of a number in memory, just as we do on paper: 123456 is one number and 123 456 are two numbers. On “paper,” we use the space character to represent the end of the number. In memory, we could do the same:

```
123456 as characters: | 1 | 2 | 3 | 4 | 5 | 6 | | ? |
123 456 as characters: | 1 | 2 | 3 | 4 | 5 | 6 |
```

The distinction between storing fixed-size binary representation (e.g., an **int**) and variable-size character string representation (e.g., a **string**) also occurs in files. By default, **iostreams** deal with character representations; that is, an **istream** reads a sequence of characters and turns it into an object of the desired type. An **ostream** takes an object of a specified type and transforms it into a sequence of characters which it writes out. However, it is possible to request **istream** and **ostream** to simply copy bytes to and from files. That’s called *binary I/O* and is requested by opening a file with the mode **ios_base::binary**. Here is an example that reads and writes binary files of integers. The key lines that specifically deal with “binary” are explained below:

```cpp
int main() {
    // open an istream for binary input from a file:
    cout << "Please enter input file name\n";
    string iname;
    cin >> iname;
    ifstream ifs (iname, ios_base::binary); // note: stream mode
    // binary tells the stream not to try anything clever with the bytes
    if (!ifs) error ("can't open input file ", iname);

    // open an ostream for binary output to a file:
    cout << "Please enter output file name\n";
    string oname;
    cin >> oname;
    ofstream ofs (oname, ios_base::binary); // note: stream mode
    // binary tells the stream not to try anything clever with the bytes
    if (!ofs) error ("can't open output file ", oname);

    vector<int> v;

    // read from binary file:
    for (int x; ifs.read(as_bytes(x), sizeof(int));) // note: reading bytes
        v.push_back(x);

    // … do something with v …

    // write to binary file:
    for (int x : v)
        ofs.write(as_bytes(x), sizeof(int)); // note: writing bytes
    return 0;
}
```

We open the files using **ios_base::binary** as the stream mode:

```cpp
ifstream ifs (iname, ios_base::binary);
ofstream ofs (oname, ios_base::binary);
```

In both cases, we chose the trickier, but often more compact, binary representation. When we move from character-oriented I/O to binary I/O, we give up our usual `>>` and `<<` operators. Those operators specifically turn values into character sequences using the default conventions (e.g., the string `"asdf"` turns into the characters **a**, **s**, **d**, **f** and the integer **123** turns into the characters **1**, **2**, **3**). If we wanted that, we wouldn’t need to say `binary` – the default would suffice. We use `binary` only if we (or someone else) thought that we somehow could do better than the default. We use `binary` to tell the stream not to try anything clever with the bytes.

What “cleverness” might we do to an `int`? The obvious is to store a 4-byte `int` in 4 bytes; that is, we can look at the representation of the `int` in memory (a sequence of 4 bytes) and transfer those bytes to the file. Later, we can read those bytes back the same way and reassemble the `int`:

```cpp
ifs.read(as_bytes(i),sizeof(int))    // note: reading bytes
ofs.write(as_bytes(vii),sizeof(int)) // note: writing bytes
```

The `ostream write()` and the `istream read()` both take an address (supplied here by `as_bytes()`) and a number of bytes (characters) which we obtained by using the operator `sizeof`. That address should refer to the first byte of memory holding the value we want to read or write. For example, if we had an `int` with the value **1234**, we would get the 4 bytes (using hexadecimal notation) **00, 00, 04, d2**:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_424_0.png)

The `as_bytes()` function is needed to get the address of the first byte of an object’s representation. It can – using language facilities yet to be explained (§17.8 and §19.3) – be defined like this:

```cpp
template<class T>
char* as_bytes(T& i)                 // treat a T as a sequence of bytes
{
    void* addr = &i;                 // get the address of the first byte
                                     // of memory used to store the object
    return static_cast<char*>(addr);  // treat that memory as bytes
}
```

The (unsafe) type conversion using `static_cast` is necessary to get to the “raw bytes” of a variable. The notion of addresses will be explored in some detail in Chapters 17 and 18. Here, we just show how to treat any object in memory as a sequence of bytes for the use of `read()` and `write()`.
