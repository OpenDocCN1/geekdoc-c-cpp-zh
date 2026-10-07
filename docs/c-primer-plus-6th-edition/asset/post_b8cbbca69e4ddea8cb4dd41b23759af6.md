
# Data Information, Constructors, and Odds and Ends 1251

The template defines a static constant:
static const size_type npos = -1;

Because size_type is unsigned, assigning the value -1 actually amounts to assigning the largest possible unsigned value to npos. This value corresponds to one greater than the largest possible array index.

# Data Information, Constructors, and Odds and Ends

Constructors can be described in terms of the effects they have. Because the private portions of a class can be implementation dependent, these effects should be described in terms of information available as part of the public interface. Table F1 lists methods whose return values can be used to describe the effects of constructors and of other methods. Note that much of the terminology is from the STL.

Table F.1 Some string Data Methods

| Method | Returns |
| --- | --- |
| begin() | An iterator to the first character in a string. |
| cbegin() | A const_iterator to the first character in a string (C++11). |
| end() | An iterator that is the past-end-value. |
| cend() | A const_iterator that is the past-end-value (C++11). |
| rbegin() | A reverse iterator that is the past-end. |
| crbegin() | A reverse const_iterator that is the past-end (C++11). |
| rend() | A reverse iterator that refers to the first character. |
| crend() | A reverse const_iterator that refers to the first character (C++11). |
| size() | The number of elements in a string, to the distance from begin() to end(). |
| length() | The same as size(). |
| capacity() | The allocated number of elements in a string. This can be greater than the actual number of characters. The value of capacity() - size() represents the number of characters that can be appended to a string before more memory is allocated. |
| max_size() | The maximum allowable size of a string. |
| data() | A pointer of type const* to the first element of an array whose first size() elements equal the corresponding elements in the string controlled by *this. The pointer should not be assumed to be valid after the string object itself has been modified. |

# 1252 Appendix F The string Template Class

| Table F.1 Some string Data Methods |
| Method | Returns |
| c_str() | A pointer of type const char* that points to the first element of an array whose first size() elements the corresponding elements in the string controlled by *this and whose next element is the charT (end-of-string marker) for the char type. The pointer should not be assumed to be valid after the string object itself has been modified. |

get_allocator() A copy of the allocator object that is used to allocate memory for the string object.

Be careful of the differences between begin(), rend(), data(), and c_str(). All relate to the first character in a string, but in different ways. The begin() and rend() methods return iterators, which are generalizations of pointers, as in Chapter 16,"The string Class and the Standard Template Library." In particular, begin() returns a model of a forward iterator, and rend() returns a copy of a reverse iterator. Refer to the actual string managed by the object (Because the string class uses dynamic memory allocation, the string contents need not be the object, so we use the term manage to describe the relationship between object and string.) You can use the methods that return iterators with iterator-based algorithms of the STL. For example, you can use the STL reverse() function to reverse the contents of a string:

```
string word;
cin >> word;
reverse(word.begin(), word.end());
```

The data() and c_str() methods, on the other hand, return ordinary pointers. Furthermore, the returned pointers point to the first element of an array that holds the string characters. This array can need not be a copy of the original string managed by the string object.(The internal representation used by the string object can be an original data, but it doesn't have to be.) It is possible that the returned pointers point to the original data, they are const, so they can't used to alter the data. Also the pointers are not guaranteed to be valid after the string is modified; this reflects that they may point to the original data. The difference between data() and c_str() is that the array c_str() points to a terminated with a null character (or equivalent), whereas data() guarantees that the actual characters are present. Thus, the c_str() method can be used, for example, as an argument to a function that expects to receive a C-style string:

```
string file("tofu.man");
ofstream outFile(file.c_str());
```

Similarly, data() and size() could be used with a function that expects to receive a pointer to an array element and a value that represents the number of elements to process:

# Data Information, Constructors, and Odds and Ends 1253

```
string vampire("Do not stake me, oh my darling!");
int vlad = byte_check(vampire.data(), vampire.size());
```

A C++ implementation could choose to represent a string object's string as a dynamically allocated C-style string and to implement the forward iterator as a pointer. In that case, the implementation could choose to have begin(), data(), and c_str() all return the same pointer. But it could just legitimately (if not easily) return references to two different data objects.

C++11 has 11 constructors for the basic_string template class, from the six of C++98, and one others:

```
explicit basic_string(const Allocator& a = Allocator());
basic_string(const char* s, const Allocator& a = Allocator());
basic_string(const char* t, size_type n, const Allocator& a = Allocator());
basic_string(const basic_string& str);
basic_string(const basic_string& str, const Allocator&);
basic_string(const basic_string& str, size_type pos,
size_type n = npos, const Allocator& a = Allocator());
basic_string(const basic_string&& str, noexcept);
basic_string(const basic_string&& str, const Allocator&);
basic_string(size_type n, const char& c, const Allocator& a = Allocator());
template<class InputIterator>
basic_string(InputIterator end,
const Allocator& a = Allocator());
basic_string(const initializer_list<char>& t, const Allocator& a = Allocator());
```

Some of the increase in constructors comes from handling arguments differently. For example, C++98 had this copy constructor:

```
basic_string(const basic_string& str, size_type pos = 0,
size_type n = npos, const Allocator& a = Allocator());
```

C++11 replaces it with three constructors--the second, third, and fourth items in the preceding list. The really new additions are the move constructors (those with rvalue references, much more efficiently. Really, as discussed in Chapter 18,"Visiting with the New C++ Standard") and the constructor with the initializer_list parameter.

Note that most constructors have an argument of the following form:

```
const Allocator& a = Allocator();
```

Recall that the term Allocator is the template parameter for an allocator to manage memory. The Allocator() is the default constructor for such class. Thus, by default, use the default version of the allocator object, but they give you the option of using some other version of the allocator object. The following sections examine the constructors individually.

# Default Constructor

This is the prototype for the default constructor:

```
explicit basic_string(const Allocator& a = Allocator());
```

Typically, you would accept the default argument for the allocator class and use the constructor to create empty strings:

string bean;
wstring theory;

The following relationships hold after the default constructor is called:

- The data() method returns a non-null pointer to 0 can be added.
- The size() method returns 0.
- The return value for capacity() is not specified.

Suppose you assign the value returned by data() to the pointer str. In this case, the first condition means str + 0 is valid.

# Constructors That Use C-Style Strings

Constructors use C-style strings let you initialize a string object from a C-style string; more generally, let you initialize a charT specialization from an array of charT values:

```
basic_string(const charT* s, const Allocator& a = Allocator());
```

To determine how many characters to copy, the constructor applies the traits::length() method to the array pointed to by s. (The pointer should not be a null pointer). For example, the following statement initializes the toast object, using the indicated string:

```
string toast("Here's looking at you, kid.");
```

The traits::length() method for type char uses the null character to determine how many characters to copy.

The following relationships hold after the constructor is called:

- The data() method returns a pointer to the first element of a copy of the array s.
- The size() method returns a value equal to traits::length().
- The capacity() method returns a value at least as large as size().

# Constructors That Use Part of a C-Style String

Constructors use part of a C-style string let you initialize a string object from part of a C-style string; more generally, let you initialize a charT specialization from part of an array of charT values:

```
basic_string(const charT* s, size_type n, const Allocator& a = Allocator());
```
