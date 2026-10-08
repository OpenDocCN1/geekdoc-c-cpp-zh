
# Exercises

- 10. Discuss how the following input problems can be resolved:
    - a. The user typing an out-of-range value
    - b. Getting no value (end of file)
    - c. The user typing something of the wrong type
- 11. In what way is input usually harder than output?
- 12. In what way is output usually harder than input?
- 13. Why do we (often) want to separate input and output from computation?
- 14. What are the two most common uses of the `istream` member function `clear()`?
- 15. What are the usual function declarations for `<<` and `>>` for a user-defined type `X`?

# Terms

- `bad()`
- `buffer`
- `clear()`
- `close()`
- device driver
- `eof()`
- `fail()`
- file
- `good()`
- `ifstream`
- input device
- input operator
- `iostream`
- `istream`
- `ofstream`
- `open()`
- `ostream`
- output device
- output operator
- stream state
- structured file
- terminator
- `unget()`

# Exercises

1. Write a program that produces the sum of all the numbers in a file of whitespace-separated integers.
2. Write a program that creates a file of data in the form of the temperature `Reading` type defined in §10.5. For testing, fill the file with at least 50 “temperature readings.” Call this program `store_temps.cpp` and the file it creates `raw_temps.txt`.
3. Write a program that reads the data from `raw_temps.txt` created in exercise 2 into a vector and then calculates the mean and median temperatures in your data set. Call this program `temp_stats.cpp`.
4. Modify the `store_temps.cpp` program from exercise 2 to include a temperature suffix *c* for Celsius or *f* for Fahrenheit temperatures. Then modify the `temp_stats.cpp` program to test each temperature, converting the Celsius readings to Fahrenheit before putting them into the vector.
5. Write the function `print_year()` mentioned in §10.11.2.
6. Define a `Roman_int` class for holding Roman numerals (as `ints`) with a `<<` and `>>`. Provide `Roman_int` with an `as_int()` member that returns the int value, so that if `r` is a `Roman_int`, we can write:
    ```cpp
    cout << "Roman" << r << " equals " << r.as_int() << "\n";
    ```
7. Make a version of the calculator from Chapter 7 that accepts Roman numerals rather than the usual Arabic ones, for example, `XXI + CIV == CXXV`.
8. Write a program that accepts two file names and produces a new file that is the contents of the first file followed by the contents of the second; that is, the program concatenates the two files.
9. Write a program that takes two files containing sorted whitespace-separated words and merges them, preserving order.
10. Add a command from `x` to the calculator from Chapter 7 that makes it take input from a file `x`. Add a command to `y` to the calculator that makes it write its output (both standard output and error output) to file `y`. Write a collection of test cases based on ideas from §7.3 and use that to test the calculator. Discuss how you would use these commands for testing.
11. Write a program that produces the sum of all the whitespace-separated integers in a text file. For example, `bears: 17 elephants 9 end` should output `26`.

# Postscript

Much of computing involves moving lots of data from one place to another, for example, copying text from a file to a screen or moving music from a computer onto an MP3 player. Often, some transformation of the data is needed on the way. The `iostream` library is a way of handling many such tasks where the data can be seen as a sequence (a stream) of values. Input and output can be a surprisingly large part of common programming tasks. This is partly because we (or our programs) need a lot of data and partly because the point where data enters a system is a place where lots of errors can happen. So, we must try to keep our I/O simple and try to minimize the chances that bad data “slips through” into our system.

# 11

# Customizing Input and Output

> “Keep it simple:
> as simple as possible,
> but no simpler.”
> —Albert Einstein

In this chapter, we concentrate on how to adapt the general `iostream` framework presented in Chapter 10 to specific needs and tastes. This involves a lot of messy details dictated by human sensibilities to what they read and also practical constraints on the uses of files. The final example shows the design of an input stream for which you can specify the set of separators.

## 11.1 Regularity and irregularity

The `iostream` library – the input/output part of the ISO C++ standard library – provides a unified and extensible framework for input and output of text. By “text” we mean just about anything that can be represented as a sequence of characters. Thus, when we talk about input and output we can consider the integer 1234 as text because we can write it using the four characters 1, 2, 3, and 4.

So far, we have treated all input sources as equivalent. Sometimes, that’s not enough. For example, files differ from other input sources (such as communications connections) in that we can address individual bytes. Similarly, we worked on the assumption that the type of an object completely determined the layout of its input and output. That’s not quite right and wouldn’t be sufficient. For example, we often want to specify the number of digits used to represent a floating-point number on output (its precision). This chapter presents a number of ways in which we can tailor input and output to our needs.

As programmers, we prefer regularity: treating all in-memory objects uniformly, treating all input sources equivalently, and imposing a single standard on the way to represent objects entering and exiting the system give the cleanest, simplest, most maintainable, and often the most efficient code. However, our programs exist to serve humans, and humans have strong preferences. Thus, as programmers we must strive for a balance between program complexity and accommodation of users’ personal tastes.

## 11.2 Output formatting

People care a lot about apparently minor details of the output they have to read. For example, to a physicist 1.25 (rounded to two digits after the dot) can be very different from **1.2467047**, and to an accountant (**1.25**) can be legally different from (**1.2467**) and totally different from **1.25** (in financial documents, parentheses are sometimes used to indicate losses, that is, negative values). As programmers, we aim at making our output as clear and as close as possible to the expectations of the “consumers” of our program. Output streams (`ostreams`) provide a variety of ways for formatting the output of built-in types. For user-defined types, it is up to the programmer to define suitable `<<` operations.

There seem to be an infinite number of details, refinements, and options for output and quite a few for input. Examples are the character used for the decimal point (usually dot or comma), the way to output monetary values, a way to represent true as the word **true** (or **vrai** or **sandt**) rather than the number **1** when output, ways to deal with non-ASCII character sets (such as Unicode), and a way to limit the number of characters read into a string. These facilities tend to be uninteresting until you need them, so we’ll leave their description to manuals and specialized works such as *Langer, Standard C++ I/OStreams and Locales*; Chapters 38 and 39 of *The C++ Programming Language* by Stroustrup; and §22 and §27 of the ISO C++ standard. Here we’ll present the most frequently useful features and a few general concepts.

### 11.2.1 Integer output

Integer values can be output as octal (the base-8 number system), decimal (our usual base-10 number system), and hexadecimal (the base-16 number system). If you don’t know about these systems, read §A.2.1.1 before proceeding here. Most output uses decimal. Hexadecimal is popular for outputting hardware-related information. The reason is that a hexadecimal digit exactly represents a 4-bit value. Thus, two hexadecimal digits can be used to present the value of an 8-bit byte, four hexadecimal digits give the value of 2 bytes (that’s often a half word), and eight hexadecimal digits can present the value of 4 bytes (that’s often the size of a word or a register). When C++’s ancestor C was first designed (in the 1970s), octal was popular for representing bit patterns, but now it’s rarely used.

We can specify the output (decimal) value **1234** to be decimal, hexadecimal (often called “hex”), and octal:

```cpp
cout << 1234 << "\t(decimal)\n"
     << hex << 1234 << "\t(hexadecimal)\n"
     << oct << 1234 << "\t(octal)\n";
```

The ‘\t’ character is “tab” (short for “tabulation character”). This prints:

**1234 (decimal)**
**4d2 (hexadecimal)**
**2322 (octal)**
