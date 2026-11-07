# # Output with cout

As mentioned previously, C++ considers output to be a stream of bytes. (Depending on the implementation and platform, these may be 8-bit, 16-bit, or 32-bit bytes, but they're bytes nonetheless.) But many kinds of data in a program are organized into larger units than a single byte. An int type, for example, may be represented by a 16-bit or 32-bit binary value. And a double value may be represented by 64 bits of binary data. But when you send a stream of bytes to a screen, you want each byte to represent a character value. That is, to display the number -2.34 onscreen, you should send the five characters -, 2, ., 3, and 4 to the screen, and not the internal 64-bit floating-point representation of that value. Therefore, one of the most important tasks facing the ostream class is converting numeric types, such as int or float, into a stream of characters that represents the values in text form. That is, the ostream class translates the internal representation of data as binary bit patterns to an output stream of character bytes. (Some day we may have bionic implants to enable us to interpret binary data directly. I leave that development as another exercise for the reader.) To perform these translation tasks, the ostream class provides several class methods. We'll look at them now, summarizing methods used throughout the book and describing additional methods that provide finer control over the appearance of the output.

# ## The Overloaded << Operator

Most often, this book has used cout with the << operator, also called the insertion operator:

```
```
int clients = 22;
cout << clients;
```
```

In C++, as in C, by default the << operator is used as the bitwise left-shift operator (see Appendix E, "Other Operators"). An expression such as x<<3 means to take the binary representation of x and shift all the bits three units to the left. Obviously, this doesn't have a lot to do with output. But the ostream class redefines the << operator through overloading to output for the ostream class. In this guise, the << operator is called the insertion operator instead of the left-shift operator. (The left-shift operator earned this new role through its visual aspect, which suggests a flow of information to the left.) The insertion operator is overloaded to recognize all the basic C++ types:

+   - unsigned char
+   - signed char
+   - char
+   - short
+   - unsigned short
+   - int
+   - unsigned int