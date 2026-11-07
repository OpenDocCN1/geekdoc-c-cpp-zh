
## The `string` Template Class

Much of this appendix is a bit technical. However, if you just want to know the capabilities of the string template class, you can concentrate on the descriptions of the various string methods.

The string class is based on a template definition:

```cpp
template<class charT, class traits = char_traits<charT>,
         class Allocator = allocator<charT> >
class basic_string {...};
```

Here `charT` represents the type stored in the string. The `traits` parameter represents a class that defines necessary properties that a type must possess to be represented as a string. For example, it should have a `length()` method that returns the length of a string, represented as an array of type `charT`. The end of such an array is indicated by the value `charT()`, the generalization of the null character. (The expression `charT(0)` is a type cast of 0 to type `charT`. It could be just 0, as it is for type char, or more generally, it could be an object created by a `charT` constructor.) The class also includes methods for comparing values, and so on. The `Allocator` parameter represents a class to handle memory allocation for the string. The default `allocator<charT>` template uses new and delete in the standard ways.

There are four predefined specializations:

```cpp
typedef basic_string<char> string;
typedef basic_string<char16_t> u16string;
typedef basic_string<char32_t> u32string;
typedef basic_string<wchar_t> wstring;
```

These specializations, in turn, use the following specializations:

```cpp
char_traits<char>
allocator<char>
char_traits<char16_t>
allocator<char16_t>
char_traits<char32_t>
allocator<char32_t>
char_traits<wchar_t>
allocator<wchar_t>
```

You can create a string class for some type other than char or wchar_t by defining a traits class and using the basic_string template.

### Thirteen Types and a Constant

The basic_string template defines several types that are used later in defining the methods:

```cpp
typedef traits                                      traits_type;
typedef typename traits::char_type                 value_type;
typedef Allocator                                  allocator_type;
typedef typename Allocator::size_type              size_type;
typedef typename Allocator::difference_type       difference_type;
typedef typename Allocator::reference             reference;
typedef typename Allocator::const_reference       const_reference;
typedef typename Allocator::pointer                pointer;
typedef typename Allocator::const_pointer         const_pointer;
```

Note that traits is a template parameter that corresponds to some specific type, such as `char_traits<char>`; `traits_type` becomes a typedef for that specific type. The following notation means that `char_type` is a type name defined in the class represented by `traits`:

```cpp
typedef typename traits::char_type              value_type;
```

The keyword `typename` is used to tell the compiler that the expression `traits::char_type` is a type. For the string specialization, for example, `value_type` is `char`.

`size_type` is used like `size_t`, except that it returns the size of a string in terms of the stored type. For the string specialization, that would be in terms of `char`, in which case `size_type` is the same as `size_t`. It is an unsigned type.

`difference_type` is used to measure the distance between two elements of a string, again in units corresponding to the size of a single element. Typically, it would be a signed version of the type underlying `size_type`.

For the char specialization, `pointer` is type `char *`, and `reference` is type `char &`. However, if you create a specialization for a type of your own design, these types (pointer and reference) could refer to classes that have the same properties as the more basic pointers and references.

To allow Standard Template Library (STL) algorithms to be used with strings, the template defines some iterator types:

```cpp
typedef (models random access iterator)        iterator;
typedef (models random access iterator)        const_iterator;
typedef std::reverse_iterator<iterator>        reverse_iterator;
typedef std::reverse_iterator<const_iterator> const_reverse_iterator;
```

The template defines a static constant:

```cpp
static const size_type npos = -1;
```

Because `size_type` is unsigned, assigning the value -1 actually amounts to assigning the largest possible unsigned value to `npos`. This value corresponds to one greater than the largest possible array index.

### Data Information, Constructors, and Odds and Ends

Constructors can be described in terms of the effects they have. Because the private portions of a class can be implementation dependent, these effects should be described in terms of information available as part of the public interface. Table F.1 lists several methods whose return values can be used to describe the effects of constructors and of other methods. Note that much of the terminology is from the STL.

**Table F.1** Some string Data Methods

| Method | Returns |
|---|---|
| `begin()` | An iterator to the first character in a string. |
| `cbegin()` | A `const_iterator` to the first character in a string (C++11). |
| `end()` | An iterator that is the past-the-end value. |
| `cend()` | A `const_iterator` that is the past-the-end value (C++11). |
| `rbegin()` | A reverse iterator that is the past-the-end. |
| `crbegin()` | A reverse `const_iterator` that is the past-the-end (C++11). |
| `rend()` | A reverse iterator that refers to the first character. |
| `crend()` | A reverse `const_iterator` that refers to the first character (C++11). |
| `size()` | The number of elements in a string, equal to the distance from `begin()` to `end()`. |
| `length()` | The same as `size()`. |
| `capacity()` | The allocated number of elements in a string. This can be greater than the actual number of characters. The value of `capacity() - size()` represents the number of characters that can be appended to a string before more memory needs to be allocated. |
| `max_size()` | The maximum allowable size of a string. |
| `data()` | A pointer of type `const charT*` that points to the first element of an array whose first `size()` elements equal the corresponding elements in the string controlled by `*this`. The pointer should not be assumed to be valid after the string object itself has been modified. |
| `c_str()` | A pointer of type `const charT*` that points to the first element of an array whose first `size()` elements equal the corresponding elements in the string controlled by `*this` and whose next element is the `charT()` character (end-of-string marker) for the `charT` type. The pointer should not be assumed to be valid after the string object itself has been modified. |
| `get_allocator()` | A copy of the allocator object that is used to allocate memory for the string object. |

Be careful of the differences among `begin()`, `rend()`, `data()`, and `c_str()`. All relate to the first character in a string, but in different ways. The `begin()` and `rend()` methods return iterators, which are generalizations of pointers, as described in Chapter 16, “The string Class and the Standard Template Library.” In particular, `begin()` returns a model of a forward iterator, and `rend()` returns a copy of a reverse iterator. Both refer to the actual string managed by the string object. (Because the string class uses dynamic memory allocation, the actual string contents need not be inside the object, so we use the term *manage* to describe the relationship between object and string.) You can use the methods that return iterators with the iterator-based algorithms of the STL. For example, you can use the STL `reverse()` function to reverse the contents of a string:

```cpp
string word;
cin >> word;
reverse(word.begin(), word.end());
```

The `data()` and `c_str()` methods, on the other hand, do return ordinary pointers. Furthermore, the returned pointers point to the first element of an *array* that holds the string characters. This array can but need not be a copy of the original string managed by the string object. (The internal representation used by the string object can be an array, but it doesn’t have to be.) Because it is possible that the returned pointers point to the original data, they are const, so they can’t be used to alter the data. Also the pointers are not guaranteed to be valid after the string is modified; this reflects that they may point to the original data. The difference between `data()` and `c_str()` is that the array `c_str()` points to is terminated with a null character (or equivalent), whereas `data()` just guarantees that the actual string characters are present. Thus, the `c_str()` method can be used, for example, as an argument to a function that expects to receive a C-style string:

```cpp
string file("tofu.man");
ofstream outFile(file.c_str());
```

Similarly, `data()` and `size()` could be used with a function that expects to receive a pointer to an array element and a value that represents the number of elements to process:
