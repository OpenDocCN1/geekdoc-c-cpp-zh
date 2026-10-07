# The string Template Class

Much of this appendix is a bit technical. However, if you just want to know the capabilities of the string template class, you can concentrate on the descriptions of the various string methods.

The string class is based on a template definition:

```
template<class charT, class traits = char_traits<charT>,
    class Allocator = allocator<charT> >
class basic_string {...};
```

Here charT represents the type stored in the string. The traits parameter represents a class that defines necessary properties that a type must possess to be represented as a string. For example, it should have a length() method that returns the length of a string, represented as an array of type charT. The end of such an array is indicated by the value charT(0), the generalization of the null character. (The expression charT(0) is a type cast of 0 to type charT. It could be just 0, as it is for type char, or more generally, it could be an object created by a charT constructor.) The class also includes methods for comparing values, and so on. The Allocator parameter represents a class to handle memory allocation for the string. The default allocator<charT> template uses new and delete in the standard ways.

There are four predefined specializations:

```
typedef basic_string<char> string;
typedef basic_string<char16_t> u16string;
typedef basic_string<char32_t> u32string;
typedef basic_string<wchar_t> wstring;
```

These specializations, in turn, use the following specializations:

```
char_traits<char>
allocator<char>
char_traits<char16_t>
allocator<char_16>
char_traits<char_32>
allocator<char_32>
char_traits<wchar_t>
allocator<wchar_t>
```