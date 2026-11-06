# 21.1 Introduction¹

+   1. Various `string` features we discuss in this chapter were also presented in Chapter 21. We kept all the features in this chapter for completeness and for people who may read the chapters out of order.

The class template `basic_string` provides typical string-manipulation operations such as copying, searching, etc. The template definition and all support facilities are defined in `namespace std`; these include the `typedef` statement

```
typedef basic_string<char> string;
```

that creates the alias type `string` for `basic_string<char>`. A `typedef` is also provided for the `wchar_t` type (`wstring`). Type `wchar_t` stores characters (e.g., two-byte characters, four-byte characters, etc.) for supporting other character sets. We use `string` exclusively throughout this chapter. To use `strings`, include header `<string>`.

+   2. Type `wchar_t` commonly is used to represent Unicode®, but `wchar_t`’s size is not specified by the standard. C++11 also has types `char16_t` and `char32_t` for Unicode support. The Unicode Standard