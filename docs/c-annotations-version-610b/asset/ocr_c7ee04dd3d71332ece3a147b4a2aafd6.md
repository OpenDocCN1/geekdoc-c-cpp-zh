is encountered, the leftmost two operands are evaluated first (cout << "hello "), and an ostream & object, which is actually the same cout object, is returned. Now, the statement is reduced to

```
```cpp
cout << "world";
```
```

and the second string is inserted into cout.

The << operator has a lot (of overloaded) variants, so many types of variables can be inserted into ostream objects. There is an overloaded <<-operator expecting an int, a double, a pointer, etc. Each operator returns the ostream object into which the information so far has been inserted, and can thus immediately be followed by the next insertion.

Streams lack facilities for formatted output like C's printf and vprintf functions. Although it is not difficult to implement these facilities in the world of streams, printf-like functionality is hardly ever required in C++ programs. Furthermore, as it is potentially type-unsafe, it might be better to avoid this functionality completely.

When binary files must be written, normally no text-formatting is used or required: an int value should be written as a series of raw bytes, not as a series of ASCII numeric characters 0 to 9. The following member functions of ostream objects may be used to write 'binary files':

+   - `ostream& put(char c):`
+     to write a single character to the output stream. Since a character is a byte, this member function could also be used for writing a single character to a text-file.
+   - `ostream& write(char const *buffer, int length):`
+     to write at most `length` bytes, stored in the `char const *buffer` to the ostream object. Bytes are written as they are stored in the buffer, no formatting is done whatsoever. Note that the first argument is a `char const *`: a type cast is required to write any other type. For example, to write an `int` as an unformatted series of byte-values use:

```
```cpp
int x;
out.write(reinterpret_cast<char const *>(&x), sizeof(int));
```
```

The bytes written by the above write call are written to the ostream in an order depending on the endian-ness of the underlying hardware. Big-endian computers write the most significant byte(s) of multi-byte values first, little-endian computers first write the least significant byte(s).

# ### 6.4.1.2 'ostream' positioning

Although not every ostream object supports repositioning, they usually do. This means that it is possible to rewrite a section of the stream which was written earlier. Repositioning is frequently used in database applications where it must be possible to access the information in the database at random.

The current position can be obtained and modified using the following members:

+   - `ios::pos_type tellp():`
+     the current (absolute) position in the file where the next write-operation to the stream will take place is returned.
+   - `ostream& seekp(ios::off_type step, ios::seekdir org):`
+     modifies a stream's actual position. The function expects an `off_type step` representing the number of bytes the current stream position is moved with respect to `org`. The `step` value may be negative, zero or positive.
+     The origin of the step, `org` is a value in the `ios::seekdir` enumeration. Its values are:
+     - `ios::beg:`
+       the stepsize is computed relative to the beginning of the stream. This value is used by default.