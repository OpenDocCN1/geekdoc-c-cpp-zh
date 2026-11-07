The non-member comparison functions are overloaded relational operators:

```
```
operator==()
operator<()
operator<=()
operator>()
operator>=()
operator!=()
```
```

Each operator is overloaded so that it can compare a string object to a string object, a C-style string, and a C-style string to a string object. These operators are defined in terms of the compare() method, so they provide a notationally more convenient way of making comparisons.

# String Modifiers

The string class provides several methods for modifying strings. Most come with an abundance of overloaded versions so that they can be used with string objects, string arrays, individual characters, and iterator ranges.

# Methods for Appending and Adding

You can append one string to another by using the overloaded += operator or by using an append() method. All throw a length_error exception if the result would be longer than the maximum string size. The += operators let you append a string object, a string array, or an individual character to another string:

```
```
basic_string& operator+=(const basic_string& str);
basic_string& operator+=(const char* s);
basic_string& operator+=(char c);
```
```

The append() methods also let you append a string object, a string array, or an individual character to another string. In addition, they let you append part of a string object by specifying an initial position and a number of characters to append or else by specifying a range. You can append part of a string by specifying how many characters of the string to use. The version for appending a character lets you specify how many instances of that character to copy. Here are the prototypes for the various append() methods:

```
```
basic_string& append(const basic_string& str);
basic_string& append(const basic_string& str, size_type pos,
                     size_type n);
template<class InputIterator>
    basic_string& append(InputIterator first, InputIterator last);
basic_string& append(const char* s);
basic_string& append(const char* s, size_type n);
basic_string& append(size_type n, charT c);   // append n copies of c
void push_back(charT c);                       // appends 1 copy of c
```
```