
## Chapter 5: The ‘string’ Data Type

C++ offers many solutions for common problems. Most of these facilities are part of the *Standard Template Library* or they are implemented as *generic algorithms* (see chapter 19).

Among the facilities C++ programmers have developed over and over again are those manipulating chunks of text, commonly called *strings*. The C programming language offers rudimentary string support. C’s *ASCII-Z* terminated series of characters form the foundation upon which an enormous amount of code has been built¹.

To process text C++ offers a `std::string` type. In C++ the traditional C library functions manipulating ASCII-Z strings are deprecated in favor of using `string` objects. Many problems in C programs are caused by buffer overruns, boundary errors and allocation problems that can be traced back to improperly using these traditional C string library functions. Many of these problems can be prevented using C++ `string` objects.

Actually, `string` objects are *class type* variables, and in that sense they are comparable to stream objects like `cin` and `cout`. In this section the use of `string` type objects is covered. The focus is on their definition and their use. When using `string` objects the *member function syntax* is commonly used:

```
stringVariable.operation(argumentList)
```

For example, if `string1` and `string2` are variables of type `std::string`, then

```
string1.compare(string2)
```

can be used to compare both strings.

In addition to the common member functions the `string` class also offers a wide variety of *operators*, like the assignment (=) and the comparison operator (==). Operators often result in code that is easy to understand and their use is generally preferred over the use of member functions offering comparable functionality. E.g., rather than writing

```
if (string1.compare(string2) == 0)
```

the following is generally preferred:

```
if (string1 == string2)
```

To define and use `string`-type objects, sources must include the header file `string`. To merely *declare* the `string` type the header should be included.

> ¹We define an ASCII-Z string as a series of ASCII-characters terminated by the ASCII-character zero (hence -Z), which has the value zero, and should not be confused with character ‘0’, which usually has the value 0x30.

### 5.1 Operations on strings

Some of the operations that can be performed on strings return indices within the strings. Whenever such an operation fails to find an appropriate index, the *value* `string::npos` is returned. This value is a symbolic value of type `string::size_type`, which is (for all practical purposes) an `(unsigned) int`.

All `string` members accepting `string` objects as arguments also accept `char const *` (C ASCII-Z string) arguments. The same usually holds true for operators accepting `string` objects.

Some `string`-members use *iterators*. Iterators are formally introduced in section [18.2]. Member functions using iterators are listed in the next section (5.2), but the iterator concept itself is not further covered by this chapter.

Strings support a large variety of members and operators. A short overview listing their capabilities is provided in this section, with subsequent sections offering a detailed discussion. The bottom line: **C++ strings** are extremely versatile and there is hardly a reason for falling back on the C library to process text. **C++ strings** handle all the required memory management and thus many related problems, which is the #1 source of problems in C programs, can be prevented when C++ strings are used. Strings do come at a price, though. The class’s extensive capabilities have also turned it into a beast. It’s hard to learn and master all its features and in the end you’ll find that not all that you expected is actually there. For example, `std::string` doesn’t offer case-insensitive comparisons. But in the end it isn’t even as simple as that. It *is* there, but it is somewhat hidden and at this point in the **C++** Annotations it’s too early to study into that hidden corner yet. Instead, realize that C’s standard library *does* offer useful functions that can be used as long as we’re aware of their limitations and are able to avoid their traps. So for now, to perform a traditional case-insensitive comparison of the contents of two `std::string` objects `str1` and `str2` the following will do:

```
strcmp(str1.c_str(), str2.c_str());
```

Strings support the following functionality:

- `initialization:` when string objects are defined they are always properly initialized. In other words, they are always in a valid state. Strings may be initialized empty or already existing text can be used to initialize strings.
- `assignment:` strings may be given new values. New values may be assigned using member functions (like `assign`) but a plain assignment operator (i.e., `=`) may also be used. Furthermore, `assignment` to a character buffer is also supported.
- `conversions:` the partial or complete contents of string objects may be interpreted as C strings but the string’s contents may also be processed as a series of raw binary bytes, not necessarily terminating in an ASCII-Z byte. Furthermore, in many situations plain characters and C strings may be used where `std::string` are accepted as well.
- `breakdown:` the individual characters stored in a string can be accessed using the familiar index operator (`[]`) allowing us to either access or modify information in the middle of a string.
- `comparisons:` strings may be compared to other strings (or C ASCII-Z strings) using the familiar logical comparison operators `==`, `!=`, `<`, `<=`, `>` and `>=`. There are also member functions available offering a more fine-grained comparison.
- `modification:` the contents of strings may be modified in many ways. Operators are available to add information to string objects, to insert information in the middle of string objects, or to replace or erase (parts of) a string’s contents.
- `swapping:` the string’s swapping capability allows us in principle to exchange the contents of two string objects without a byte-by-byte copying operation of the string’s contents.
- `searching:` the locations of characters, sets of characters, or series of characters may be searched for from any position within the string object and either searching in a forward or backward direction.
- `housekeeping:` several housekeeping facilities are offered: the string’s length, or its empty-state may be interrogated. But string objects may also be resized.
- `stream I/O:` strings may be extracted from or inserted into streams. In addition to plain string extraction a line of a text file may be read without running the risk of a buffer overrun. Since extraction and insertion operations are stream based the I/O facilities are *device independent*.

### 5.2 A `std::string` reference

In this section the string members and string-related operations are referenced. The subsections cover, respectively the string’s initializers, iterators, operators, and member functions. The following terminology is used throughout this section:

- `object` is always a `string`-object;
- `argument` is a `string const &` or a `char const *` unless indicated otherwise. The contents of an argument never is modified by the operation processing the argument;
- `opos` refers to an offset into an `object` string;
- `apos` refers to an offset into an `argument`;
- `on` represents a number of characters in an `object` (starting at `opos`);
- `an` represents a number of characters in an `argument` (starting at `apos`).

Both `opos` and `apos` must refer to existing offsets, or an exception (cf. chapter 10) is generated. In contrast, `an` and `on` may exceed the number of available characters, in which case only the available characters are considered.

Many members declare default values for `on`, `an` and `apos`. Some members declare default values for `opos`. Default offset values are 0, the default values of `on` and `an` is `string::npos`, which can be interpreted as ‘the required number of characters to reach the end of the string’.

With members starting their operations at the end of the string object’s contents proceeding backwards, the default value of `opos` is the index of the object’s *last* character, with `on` by default equal to `opos + 1`, representing the length of the substring *ending at opos*.

In the overview of member functions presented below it may be assumed that all these parameters accept default values unless indicated otherwise. Of course, the default argument values cannot be used if a function requires additional arguments beyond the ones otherwise accepting default values.
