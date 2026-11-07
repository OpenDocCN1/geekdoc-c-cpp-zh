
If the `ifstream` and `ofstream` constructors and the open() methods each take two arguments, how have we gotten by using just one in the previous examples? As you have probably guessed, the prototypes for these class member functions provide default values for the second argument (the file mode argument). For example, the `ifstream open()` method and constructor use `ios_base::in` (open for reading) as the default value for the mode argument, and the `ofstream open()` method and constructor use `ios_base::out | ios_base::trunc` (open for writing and truncate the file) as the default. The bitwise OR operator (`|`) is used to combine two bit values into a single value that can be used to set both bits. The `fstream` class doesn’t provide a mode default, so you have to provide a mode explicitly when creating an object of that class.

Note that the `ios_base::trunc` flag means an existing file is truncated when opened to receive program output; that is, its previous contents are discarded. Although this behavior commendably minimizes the danger of running out of disk space, you can probably imagine situations in which you don’t want to wipe out a file when you open it. Of course, C++ provides other choices. If, for example, you want to preserve the file contents and add (append) new material to the end of the file, you can use the `ios_base::app` mode:

```
ofstream fout("bagels", ios_base::out | ios_base::app);
```

Again, the code uses the `|` operator to combine modes. So `ios_base::out | ios_base::app` means to invoke both the out mode and the app mode (see Figure 17.6). You can expect to find some differences among older C++ implementations. For example, some allow you to omit the `ios_base::out` in the previous example, and some don’t. If you aren’t using the default mode, the safest approach is to provide all the mode elements explicitly. Some compilers don’t support all the choices in Table 17.6, and some may offer choices beyond those in the table. One consequence of these differences is that you may have to make some alterations in the following examples to use them on your system. The good news is that the development of the C++ Standard is providing greater uniformity.

Standard C++ defines parts of file I/O in terms of ANSI C standard I/O equivalents. A C++ statement like

```
ifstream fin(filename, c++mode);
```

is implemented as if it uses the C fopen() function:

```
fopen(filename, cmode);
```

Here `c++mode` is a type openmode value, such as `ios_base::in`, and `cmode` is the corresponding C-mode string, such as "r". Table 17.8 shows the correspondence between C++ modes and C modes. Note that `ios_base::out` by itself causes truncation but that it doesn’t cause truncation when combined with `ios_base::in`. Unlisted combinations, such as `ios_base::in | ios_base::trunc`, prevent the file from being opened. The `is_open()` method detects this failure.

![](img/9afc44517b591d64e2e19f623c9308ef_1138_0.png)

Figure 17.6 Some file-opening modes.

### Table 17.8 C++ and C File-Opening Modes

| C++ mode | C mode | Meaning |
| --- | --- | --- |
| `ios_base::in` | `"r"` | Open for reading. |
| `ios_base::out` | `"w"` | (Same as `ios_base::out \| ios_base::trunc`.) |
| `ios_base::out \| ios_base::trunc` | `"w"` | Open for writing, truncating file if it already exists. |
| `ios_base::app` | `"a"` | Open for writing, append only. |
| `ios_base::in \| ios_base::out` | `"r+"` | Open for reading and writing, with writing permitted anywhere in the file. |
| `ios_base::in \| ios_base::out \| ios_base::trunc` | `"w+"` | Open for reading and writing, first truncating file if it already exists. |
| `c++mode \| ios_base::binary` | `"cmodeb"` | Open in `c++mode` or corresponding `cmode` and in binary mode; for example, `ios_base::in \| ios_base::binary` becomes `"rb"`. |
| `c++mode \| ios_base::ate` | `"cmode"` | Open in indicated mode and go to end of file. C uses a separate function call instead of a mode code. For example, `ios_base::in \| ios_base::ate` translates to the `"r"` mode and the C function call `fseek(file, 0, SEEK_END)`. |

Note that both `ios_base::ate` and `ios_base::app` place you (or, more precisely, a file pointer) at the end of the file just opened. The difference between the two is that the `ios_base::app` mode allows you to add data to the end of the file only, while the `ios_base::ate` mode merely positions the pointer at the end of the file.

Clearly, there are many possible combinations of modes. We’ll look at a few representative ones.

## Appending to a File

Let’s look at a program that appends data to the end of a file. The program maintains a file that contains a guest list. When the program begins, it displays the current contents of the file, if it exists. It can use the `is_open()` method after attempting to open the file to check whether the file exists. Next, the program opens the file for output, using the `ios_base::app` mode. Then it solicits input from the keyboard to add to the file. Finally, the program displays the revised file contents. Listing 17.18 illustrates how to accomplish these goals. Note how the program uses the `is_open()` method to test whether the file has been opened successfully.

> **Note**
>
> File I/O was perhaps the least standardized aspect of C++ in its earlier days, and many older compilers don’t quite conform to the current standard. Some, for example, used modes such as `nocreate` that are not part of the current standard. Also, only some compilers require the `fin.clear()` call before opening the same file a second time for reading.

### Listing 17.18 `append.cpp`

```cpp
// append.cpp -- appending information to a file
#include <iostream>
#include <fstream>
#include <string>
#include <cstdlib>       // (for exit())

const char * file = "guests.txt";
int main()
{
    using namespace std;
    char ch;

// show initial contents
    ifstream fin;
    fin.open(file);

    if (fin.is_open())
    {
        cout << "Here are the current contents of the "
            << file << " file:\n";
        while (fin.get(ch))
            cout << ch;
        fin.close();
    }

// add new names
    ofstream fout(file, ios::out | ios::app);
    if (!fout.is_open())
    {
        cerr << "Can't open " << file << " file for output.\n";
        exit(EXIT_FAILURE);
    }

    cout << "Enter guest names (enter a blank line to quit):\n";
    string name;
    while (getline(cin,name) && name.size() > 0)
    {
        fout << name << endl;
    }
    fout.close();

// show revised file
    fin.clear();    // not necessary for some compilers
    fin.open(file);
    if (fin.is_open())
    {
        cout << "Here are the new contents of the "
            << file << " file:\n";
        while (fin.get(ch))
            cout << ch;
        fin.close();
    }
    cout << "Done.\n";
    return 0;
}
```

Here’s a sample first run of the program in Listing 17.18:

```text
Enter guest names (enter a blank line to quit):
Genghis Kant
Hank Attila
Charles Bigg

Here are the new contents of the guests.txt file:
Genghis Kant
Hank Attila
Charles Bigg
Done.
```

At this point the guests.txt file hasn’t been created, so the program doesn’t preview the file.

Next time the program is run, however, the guests.txt file does exist, so the program does preview the file. Also note that the new data are appended to the old file contents rather than replacing them:

```text
Here are the current contents of the guests.txt file:
Genghis Kant
Hank Attila
Charles Bigg
Enter guest names (enter a blank line to quit):
Greta Greppo
LaDonna Mobile
Fannie Mae

Here are the new contents of the guests.txt file:
Genghis Kant
Hank Attila
Charles Bigg
Greta Greppo
LaDonna Mobile
Fannie Mae
Done.
```

You should be able to read the contents of guests.txt with any text editor, including the editor you use to write your source code.

## Binary Files

When you store data in a file, you can store the data in text form or in binary format. Text form means you store everything as text, even numbers. For example, storing the value -2.324216e+07 in text form means storing the 13 characters used to write this number. That requires converting the computer’s internal representation of a floating-point number to character form, and that’s exactly what the << insertion operator does. Binary format, on the other hand, means storing the computer’s internal representation of a value.
