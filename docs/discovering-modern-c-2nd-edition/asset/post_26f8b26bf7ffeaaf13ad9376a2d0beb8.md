
The example also demonstrates that we can print an argument multiple times.

Reordering arguments is very important in multilingual software to provide a natural phrasing. In Section 1.3.1 we printed the average of two values, and now we want to extend this example to five languages:

Click here to view code image

```
void print_average(float v1, float v2, int language)
{
    using namespace fmt;
    string formats[] = {
        "The average of {v1} and {v2} is {result}.\n",
        "{result:.6f} ist der Durchschnitt von {v1} und {v2}.\n",
        "La moyenne de {v1} et {v2} est {result}.\n",
        "El promedio de {v1} y {v2} es {result}.\n",
        "{result} corrisponde alla media di {v1} e {v2}.\n";
    print (formats[language], "v1"_a= v1, "v2"_a= v2,
           "result"_a= (v1+v2)/2.0f);
}
```

Of course, the German version is the most pedantic one, requesting six decimal digits no matter what:

Click here to view code image

```
The average of 3.5 and 7.3 is 5.4.
5.400000 ist der Durchschnitt von 3.5 und 7.3.
La moyenne de 3.5 et 7.3 est 5.4.
El promedio de 3.5 y 7.3 es 5.4.
5.4 corrisponde alla media di 3.5 e 7.3.
```

Admittedly, this example would have worked without reordering the arguments but it nicely demonstrates the important possibility to separate the text and the formatting from the values. To store formatted text in a string we don't need a stringstream any longer but can do it directly with the function `format`.

Altogether, the new formatting is:

- Compact, as demonstrated in the examples above
- Adaptable to various output orders
- Type-safe, as an exception is thrown when an argument doesn't match
- Extensible, which we will see in Section 3.5.6

For those reasons, it is superior to the preceding techniques, and we therefore strongly advise using it as soon as sufficient compiler support is available.

## 1.7.7 Dealing with I/O Errors

To make one thing clear from the beginning: I/O in C++ is not fail-safe. Errors can be reported in different ways and our error handling must comply to them. Let us try the following example program:

![](img/5682e787fc967e93d7e33e8bac5f58a0_103_0.png)

```
int main ()
{
    std::ifstream infile("some_missing_file.xyz");

    int i;
    double d;
    infile >> i >> d;

    std::cout << "i is " << i << ", d is " << d << '\n';
    infile.close();
}
```

Although the file does not exist, the opening operation does not fail. We can even read from the nonexisting file and the program goes on. It is needless to say that the values in `i` and `d` are nonsense:

i is 1, d is 2.3452e-310

By default, the streams do not throw exceptions. The reason is historical: they are older than the exceptions, and later the behavior was kept to not break software written in the meantime. Another argument is that failing I/O is nothing exceptional but quite common, and checking errors (after each operation) would be natural.

To be sure that everything went well, we have to check error flags, in principle, after each I/O operation. The following program asks the user for new filenames until a file can be opened. After reading its content, we check again for success:

![](img/5682e787fc967e93d7e33e8bac5f58a0_103_1.png)

Click here to view code image

```
int main ()
{
    std::ifstream infile;
    std::string filename{"some_missing_file.xyz"};
    bool opened= false;
    while (!opened) {
        infile.open(filename);
        if (infile.good()) {
            opened= true;
        } else {
            std::cout << "The file '"<< filename
                      << "' doesn't exist (or can't be
                      opened), "
                      << "please give a new filename: ";
            std::cin >> filename;
        }
    }
    int i;
    double d;
    infile >> i >> d;
    if (infile.good())
        std::cout << "i is " << i << ", d is " << d << '\n';
    else
        std::cout << "Could not correctly read the
                    content.\n";
    infile.close();
}
```

You can see from this simple example that writing robust applications with file I/O can create some work. If we want to use exceptions, we have to enable them during run time for each stream:

Click here to view code image

```
cin.exceptions(ios_base::badbit | ios_base::failbit);
cout.exceptions(ios_base::badbit | ios_base::failbit);
```

```
std::ifstream infile("f.txt");
infile.exceptions(ios_base::badbit | ios_base::failbit);
```

The streams throw an exception every time an operation fails or when they are in a “bad” state. Exceptions could be thrown at (unexpected) file end as well. However, the end of file is more conveniently handled by testing (e.g., while (!f.eof())).

In the preceding example, the exceptions for infile are only enabled after opening the file (or the attempt thereof). For checking the opening operation, we have to create the stream first, then turn on the exceptions, and finally open the file explicitly. Enabling the exceptions gives us at least the guarantee that all I/O operations went well when the program terminates properly. We can make our program more robust by catching possible exceptions.

The exceptions in file I/O only protect us partially from making errors. For instance, the following small program is obviously wrong (types don't match and numbers aren't separated):

Click here to view code image

```
void with_io_exceptions(ios& io)
{
    io.exceptions(ios_base::badbit | ios_base::failbit); }
int main ()
{
    std::ofstream outfile;
    with_io_exceptions(outfile);
    outfile.open("f.txt");
    double o1= 5.2, o2= 6.2;
    outfile << o1 << o2 << std::endl; // no separation
    outfile.close();
    std::ifstream infile;
    with_io_exceptions(infile);
    infile.open("F.txt");
    int i1, i2;
    char c;
    infile >> i1 >> c >> i2; // mismatching types
    std::cout << "i1 = " << i1 << ", i2 = " << i2 << "\n";
}
```

Nonetheless, it does not throw exceptions and fabricates the following output:

i1 = 5, i2 = 26

As we all know, testing does not prove the correctness of a program. This is even more obvious when I/O is involved. Stream input reads the incoming characters and passes them as values of the corresponding variable type, e.g., `int` when setting `i1`. It stops at the first character that cannot be part of the value, first at the dot for the `int` value `i1`. If we read another `int` afterward, it would fail because an empty string cannot be interpreted as an `int` value. But we do not; instead we read a `char` next to which the dot is assigned. When parsing the input for `i2` we find first the fractional part from `01` and then the integer part from `02` before we get a character that cannot belong to an `int` value.

Unfortunately, not every violation of the grammatical rules causes an exception in practice: `.3` parsed as an `int` yields zero (while the next input probably fails); `-5` parsed as an `unsigned` results in 4294967291 (when `unsigned` is 32 bits long). The narrowing principle apparently has not found its way into I/O streams yet (if it ever will for backward compatibility’s sake).

At any rate, the I/O part of an application needs close attention. Numbers must be separated properly (e.g., by spaces) and read with the same type as they were written. Floating-point values can also vary in their local representation and it is therefore recommended to store and read them without internationalization (i.e., with neutral C locale) when the program will run on different systems. Another challenge can be branches in the output so that the file format can vary. The input code is considerably more complicated and might even be ambiguous.

There are two other forms of I/O we want to mention: binary and C-style I/O. The interested reader will find them in Sections A.2.6 and A.2.7, respectively. You can also read this later when you need it.

## C++17 1.7.8 Filesystem

=> c++17/filesystem_example.cpp

A library that was overdue in C++ is `<filesystem>`. Now we can list all files in a directory and ask for their type, for instance:¹⁶

Click here to view code image

```
namespace fs = std::filesystem;
for (auto & p : fs::directory_iterator("."))
```
