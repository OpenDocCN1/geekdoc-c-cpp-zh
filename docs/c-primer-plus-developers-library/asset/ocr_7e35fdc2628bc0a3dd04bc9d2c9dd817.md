# Constructor That Uses n Copies of a Character

A constructor that uses n copies of a character creates a string object that consists of n consecutive characters, all having the value c:

```
```cpp
basic_string(size_type n, charT c, const Allocator& a = Allocator());
```
```

This constructor requires that n < npos. If n equals npos, the constructor throws an out_of_range exception. Otherwise, the following relationships hold after the constructor is called:

+   - The `data()` method returns a pointer to the first element of a string of n elements, each set to c.
+   - The `size()` method returns n.
+   - The `capacity()` method returns a value at least as large as `size()`.

# Constructor That Uses a Range

A constructor that uses a range uses an iterator-defined range in the style of the STL:

```
```cpp
template<class InputIterator>
basic_string(InputIterator begin, InputIterator end,
            const Allocator& a = Allocator());
```
```

The begin iterator points to the element in the source at which copying begins, and end points to one past the last location to be copied.

You can use this form with arrays, strings, or STL containers:

```
```cpp
char cole[40] = "Old King Cole was a merry old soul.";
string title(cole + 4, cole + 8);
vector<char> input;
char ch;
while (cin.get(ch) && ch != '\n')
    input.push_back(ch);
string str_input(input.begin(), input.end());
```
```

In the first use, InputIterator is evaluated to type `const char *`. In the second use, InputIterator is evaluated to type `vector<char>::iterator`.

The following relationships hold after the constructor is called:

+   - The `data()` method returns a pointer to the first element of a string formed by copying elements from the range `[begin, end)`.
+   - The `size()` method returns the distance between begin and end. (The distance is measured in units equal to the size of the data type obtained when the iterator is dereferenced.)
+   - The `capacity()` method returns a value at least as large as `size()`.