
write_something(mystream);
std::cout << "mystream is: " << mystream.str(); // newline contained
}
```

Likewise, generic input can be implemented with istream and read/write I/O with iostream.

## 1.7.5 Formatting

```
=> c++03/formatting.cpp
```

I/O streams are formatted by so-called I/O manipulators which are found in the header file <iomanip>. By default, C++ only prints a few digits of floating-point numbers. Thus, we increase the precision:

```
double pi = M_PI;
cout << "pi is " << pi << '\n';
cout << "pi is " << setprecision(16) << pi << '\n';
```

and yield a more accurate number:

```
pi is 3.14159
pi is 3.141592653589793
```

In Section 4.3.1, we will show how the precision can be adjusted to the type's representable number of digits.

When we write a table, vector, or matrix, we need to align values for readability. Therefore, we next set the width of the output:

```
cout << "pi is " << setw(30) << pi << '\n';
```

This results in

```
pi is         3.141592653589793
```

setw changes only the next output while setprecision affects all following (numerical) outputs, like the other manipulators. The provided width is understood as a minimum, and if the printed value needs more space, our tables will get ugly.

We can further request that the values be left aligned, and the empty space be filled with a character of our choice, say, -:

```
cout << "pi is " << setfill('-') << left
     << setw(30) << pi << '\n';
```

yielding

```
pi is 3.141592653589793--------------
```

Another way of formatting is setting the flags directly. Some less frequently used format options can only be set this way, e.g., whether the sign is shown for positive values as well. Furthermore, we force the "scientific" notation in the normalized exponential representation:

```
cout.setf(ios_base::showpos);
cout << "pi is " << scientific << pi << '\n';
```

resulting in

```
pi is +3.1415926535897931e+08
```

Integer numbers can be represented in octal and hexadecimal base by

```
cout << "63 octal is " << oct << 63 << "\n";
cout << "63 hexadecimal is " << hex << 63 << "\n";
cout << "63 decimal is " << dec << 63 << "\n";
```

with the expected output:

```
63 octal is 77
63 hexadecimal is 3f
63 decimal is 63
```

Boolean values are by default printed as integers 0 and 1. On demand, we can present them as true and false:

```
cout << "pi < 3 is " << (pi < 3) << "\n";
cout << "pi < 3 is " << boolalpha << (pi < 3) << "\n";
```

Finally, we can reset all the format options that we changed:

```
int old_precision= cout.precision();
cout << setprecision(16)
...
cout.unsetf(ios_base::adjustfield | ios_base::basefield
| ios_base::floatfield | ios_base::showpos | ios_base::boolalpha);
cout.precision(old_precision);
```

Each option is represented by a bit in a status variable. To enable multiple options, we can combine their bit patterns with a binary OR.

## 1.7.6 Dealing with I/O Errors

To make one thing clear from the beginning: I/O in C++ is not fail-safe (let alone idiot-proof). Errors can be reported in different ways and our error handling must comply to them. Let us try the following example program:

```
int main ()
{
    std::ifstream infile("some_missing_file.xyz");
    int i;
    double d;
    infile >> i >> d;
    std::cout << "i is " << i << ", d is " << d << "\n";
    infile.close();
}
```

Although the file does not exist, the opening operation does not fail. We can even read from the non-existing file and the program goes on. Needless to say that the values in i and d are nonsense:

```
i is i, d is 2.3452e-310
```

By default, the streams do not throw exceptions. The reason is historical: they are older than the exceptions and later the behavior was kept to not break software written in the meantime.

To be sure that everything went well, we have to check error flags, in principle, after each I/O operation. The following program asks the user for new file names until a file can be opened. After reading its content, we check again for success:

```
int main ()
{
    std::ifstream infile;
    std::string filename("some_missing_file.xyz");
    bool opened = false;
    while (!opened) {
        infile.open(filename);
        if (infile.good()) {
            opened = true;
        } else {
            std::cout << "The file " << filename
                      << " doesn't exist, give a new file name: ";
            std::cin >> filename;
        }
    }
    int i;
    double d;
    infile >> i >> d;
    if (infile.good())
        std::cout << "i is " << i << ", d is " << d << '\n';
    else
        std::cout << "Could not correctly read the content.\n";
    infile.close();
}
```

You can see from this simple example that writing robust applications with file I/O can create some work.

If we want to use exceptions, we have to enable them during run time for each stream:

```
cin.exceptions(ios_base::badbit | ios_base::failbit);
cout.exceptions(ios_base::badbit | ios_base::failbit);

std::ifstream infile("f.txt");
infile.exceptions(ios_base::badbit | ios_base::failbit);
```

The streams throw an exception every time an operation fails or when they are in a "bad" state. Exceptions could be thrown at (unexpected) file end as well. However, the end of file is more conveniently handled by testing (e.g., while (!eof())).

In the example above, the exceptions for infile are only enabled after opening the file (or the attempt thereof). For checking the opening operation, we have to create the stream first, then turn on the exceptions and finally open the file explicitly. Enabling the exceptions gives us at least the guarantee that all I/O operations went well when the program terminates properly. We can make our program more robust by catching exceptions that might be thrown.

The exceptions in file I/O only protect us partially from making errors. For instance, the following small program is obviously wrong (types don't match and numbers aren't separated):

```
void with_io_exceptions(ios& io)
{
    io.exceptions(ios_base::badbit | ios_base::failbit); }

int main ()
{
    std::ofstream outfile;
    with_io_exceptions(outfile);
    outfile.open("f.txt");

    double o1 = 5.2, o2 = 6.2;
    outfile << o1 << o2 << std::endl; // no separation
    outfile.close();

    std::ifstream infile;
    with_io_exceptions(infile);
    infile.open("f.txt");

    int i1, i2;
    char c;
    infile >> i1 >> c >> i2; // mismatching types
    std::cout << "i1 = " << i1 << ", i2 = " << i2 << "\n";
}
```

Nonetheless, it does not throw exceptions and fabricates the following output:

```
i1 = 5, i2 = 26
```

As we all know, testing does not prove the correctness of a program. This is even more obvious when I/O is involved. Stream input reads the incoming characters and passes them as values of the appropriate variable type, e.g., int when setting i1. It stops at the first character that cannot be part of the value, first at the . for the int value i1. If we read another int afterward, it would fail because an empty string cannot be interpreted as an int value. But we do not; instead we read a char next to which the dot is assigned. When parsing the input for i2 we find first the fractional part from o1 and then the integer part from o2 before we get a character that cannot belong to an int value.

Unfortunately, not every violation of the grammatical rules causes an exception in practice: 3 parsed as an int yields zero (while the next input probably fails): -5 parsed as an unsigned results in 4294967291 (when unsigned is 32 bits long). The narrowing principle apparently has not found its way into I/O streams yet (if it ever will for backward compatibility's sake).

At any rate, the I/O part of an application needs utter attention. Numbers must be separated properly (e.g., by spaces) and read with the same type as they were written. When the output contains branches such that the file format can vary, the input code is considerably more complicated and might even be ambiguous.
