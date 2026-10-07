
## Data Information, Constructors, and Odds and Ends 1255

This constructor copies to the constructed object total of n characters from the array pointed to by s. Note that it doesn't stop copying if s has fewer characters than n. If n exceeds the length of s, the constructor interprets the contents of following the string as if they held that data char.

This constructor requires that s is not a null pointer and that n < npos. (Recall that npos is a static constant equal to the maximum possible number of elements in a string.) If n equals npos, the constructor throws an out_of_range exception. (Because n is of type size_type and npos is the maximum size_value, n cannot be greater than npos.) Otherwise, the following relationships hold after the constructor is called:

* The data() returns a pointer to the first element of a copy of the array s.
* The size() method returns n.
* The capacity() method returns a value at least as large as size().

### Constructors That Use An Lvalue Reference

The copy constructor looks like this:
basic_string(const basic_string& str);

It initializes a new string object using a string argument:
string mel("I'm ok!");
string ida(mel);
Here, ida would get a copy of the string managed by mel.
The next constructor additionally requires that you use an allocator:
basic_string(const basic_string& str, const Allocator&);

The relationships hold after either of these two constructors is called:

* The data() method returns a pointer to an allocated copy of the array whose element is pointed to by str.data().
* The size() method returns the value of size().
* The capacity() method returns a value at least as large as size().

Moving along, the next constructor sets several items:
basic_string(const basic_string& str, size_type pos, size_type n = npos,
const Allocator& a = Allocator());
The second argument pos specifies a location in the source string from which to begin the copying:
string att("Telephone home.");
string et(att, 4);

Position numbers begin with 0, so position 4 is the p character. Thus, et is initialized to "phone home.".

## 1256 Appendix F The string Template Class

The optional third argument n specifies the maximum number of characters to len to copy. Thus, this initializes pt to the string "phone":

```
string at("Telephone home.");
string pt(att, 4, 5);
```

However, this constructor does not pass the lesser of the source string; for example, the following steps after copying the period:

```
string pt(att, 4, 200);
```

Thus, the constructor actually copies a number of characters equal to the lesser of n and str.size() - pos. This constructor requires pos <= str.size()—that is, the initial position copied to is inside the source string; if this is not the case, the constructor throws an out_of_range exception. Otherwise, copy_len represents the lesser of n and str.size() - pos, the following relationships hold after the constructor is called:

* The data() method returns a pointer to a copy of copy_len elements copied from the string str, with position pos in str.
* The size() method returns a value at least as large as size().
* The capacity() method returns a value at least as large as size().

### Constructors That Use Rvalue Reference (C++11)

C++11 adds move semantics to the string class. As described in Chapter 18, this involves adding a move constructor, which uses an rvalue reference instead of an lvalue reference:

```
basic_string(basic_string&& str) noexcept;
```

This constructor is invoked when the actual argument is a temporary object:

```
string one("din"); // // copy constructor
string two(one); // copy constructor - one is an lvalue
string three(one+two); // move constructor, sum is an rvalue
```

As discussed in Chapter 18, the intent is that string three takes ownership of the object created by operator+() rather than copying the object and letting the original be destroyed.

The second rvalue constructor additionally allows you to specify an allocator:
basic_string(const basic_string&& str, const Allocator&);

The following relationships hold after either of these two constructors is called:

* The data() method returns a pointer to an allocated copy of the array whose first element is pointed to by str.data().
* The size() method returns the value of str.size().
* The capacity() method returns a value at least as large as size().

## Data Information, Constructors, and Odds and Ends

1257

### Constructor That Uses n Copies of a Character

A constructor that uses n copies of a character creates a string object that consists of n consecutive characters, all having the value c:

```
basic_string(size_type n, char c, const Allocator& a = Allocator());
```

This constructor requires that n < npos. If equals npos, the constructor throws an out_of_range exception. Otherwise, the following relationships hold after the constructor is called:

* The data() method returns a pointer to the first element of a string of n elements, each set to c.
* The size() method returns a value at least as large as size.
* The capacity() method returns a value at least as large as size().

### Constructor That Uses a Range

A constructor that uses a range uses an iterator-defined range in the style of the STL:

```
template<class InputIterator>
basic_string(InputIterator begin, InputIterator end,
const Allocator& a = Allocator());
```

The begin iterator points to the element in the source at copying begins, and end points to one past the last location to be copied.
You can use this with arrays, strings, or STL containers:

```
char col[40] = "Old King Cole was a merry old soul."
string title(col + 4, col + 8);
vector<char> input;
char ch;
while (cin.get(ch) && ch != '\n')
    input.push_back(ch);
string str_input(input.begin(), input.end());
```

In the first use, InputIterator is evaluated to type const char *. In the second use, InputIterator is evaluated to type vector<char>::iterator.
The following relationships hold after the constructor is called:

* The data() method returns a pointer to the first element of a string formed by copying elements from the range [begin, end).
* The size() method returns the distance between begin and end. (The distance is measured in units equal to the size of type obtained when the iterator is dereferenced.)
* The capacity() method returns a value at least as large as size().

### Constructor That Uses an initializer_list (C++11)

This constructor takes an `initializer_list<charT>` parameter:

basic_string(initializer_list<charT> il, const Allocator& a = Allocator());

You can use it with brace list of characters:

string slow({'s', 'n', 'a', 'i', 'l'});

This isn't the most convenient way to initialize a string, but it keeps the string interface similar to that of the STL container classes.

The initializer_list class has begin() and end() members, and the effect of this constructor is the same using the range constructor:

basic_string(il.begin(), il.end(), a);

### Memory Miscellany

Several methods deal with memory—for example, clearing memory contents, resizing a string, or adjusting the capacity of a string. Table F.2 lists some memory-related methods.

### Table F.2 Some Memory-Related Methods

| Method | Effect |
|---|---|
| void resize(size_type n) | Throws an out_of_range exception if n > npos. Otherwise, changes the size of a string to n, truncating the end of the string if n < size() and padding the string with charT(0) characters if n > size(). |
| void resize(size_type n, charT c) | Throws an out_of_range exception if n > npos. Otherwise, changes the size of a string to n, truncating the end of the string if n < size() and padding the string with character if n > size(). |
| void reserve(size_type res_arg = 0) | Sets capacity to greater than or equal to res_arg. Because this reallocates the string, it voids previous references, iterators, and pointers into the string. |
| void shrink_to_fit() | Non-binding request to capacity() to size() (C++11). |
| void clear() noexcept | Removes all characters from a string. |
| bool empty() const noexcept | Returns true if size() == 0. |

