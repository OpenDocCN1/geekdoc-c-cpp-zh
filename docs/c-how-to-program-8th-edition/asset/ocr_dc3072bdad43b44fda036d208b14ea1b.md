member function **tie** to synchronize (i.e., “tie together”) the operation of an istream and an ostream to ensure that outputs appear before their subsequent inputs. The call

```
```cpp
cin.tie( &cout );
```
```

ties cout (an ostream) to cin (an istream). Actually, this particular call is redundant, because C++ performs this operation automatically to create a user’s standard input environment. However, the user would tie other istream/ostream pairs explicitly. To untie an input stream, inputStream, from an output stream, use the call

```
```cpp
inputStream.tie( 0 );
```
```

# 15.10 Wrap-Up

This chapter summarized how C++ performs input/output using streams. You learned about the stream-I/O classes and objects, as well as the stream I/O template class hierarchy. We discussed ostream’s formatted and unformatted output capabilities performed by the put and write functions. You saw examples using istream’s formatted and unformatted input capabilities performed by the eof, get, getline, peek, putback, ignore and read functions. We discussed stream manipulators and member functions that perform formatting tasks—dec, oct, hex and setbase for displaying integers; precision and setprecision for controlling floating-point precision; and width and setw for setting field width. You also learned additional formatting istream manipulators and member functions—showpoint for displaying decimal point and trailing zeros; left, right and internal for justification; fill and setfill for padding; scientific and fixed for displaying floating-point numbers in scientific and fixed notation; uppercase for uppercase/lowercase control; boolalpha for specifying boolean format; and flags and fmtflags for resetting the format state.

We introduced exception handling earlier in the book in our discussion of arrays. In the next chapter, we take a deeper look at C++’s rich set of exception handling capabilities.

# Summary

*Section 15.1 Introduction*

+   - I/O operations are performed in a manner sensitive to the type of the data.

*Section 15.2 Streams*

+   - C++ I/O occurs in streams (p. 597). A stream is a sequence of bytes.
+   - Low-level I/O capabilities specify that bytes should be transferred device-to-memory or memory-to-device. High-level I/O is performed with bytes grouped into meaningful units such as integers, strings and user-defined types.
+   - C++ provides both unformatted-I/O and formatted-I/O operations. Unformatted-I/O (p. 597) transfers are fast, but process raw data that is difficult for people to use. Formatted I/O processes data in meaningful units, but requires extra processing time that can degrade the performance.
+   - The `<iostream>` header declares all stream-I/O operations (p. 598).
+   - The `<iomanip>` header declares the parameterized stream manipulators (p. 598).
+   - The `<fstream>` header declares file-processing operations (p. 600).
+   - The basic_istream template (p. 598) supports stream-input operations.