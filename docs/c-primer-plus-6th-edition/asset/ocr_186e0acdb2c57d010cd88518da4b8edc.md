You can create a string class for some type other than char or wchar_t by defining a traits class and using the basic_string template.

# Thirteen Types and a Constant

The basic_string template defines several types that are used later in defining the methods:

```
typedef traits traits_type;
typedef typename traits::char_type value_type;
typedef Allocator allocator_type;
typedef typename Allocator::size_type size_type;
typedef typename Allocator::difference_type difference_type;
typedef typename Allocator::reference reference;
typedef typename Allocator::const_reference const_reference;
typedef typename Allocator::pointer pointer;
typedef typename Allocator::const_pointer const_pointer;
```

Note that traits is a template parameter that corresponds to some specific type, such as char_traits<char>; traits_type becomes a typedef for that specific type. The following notation means that char_type is a type name defined in the class represented by traits:

```
typedef typename traits::char_type value_type;
```

The keyword typename is used to tell the compiler that the expression traits::char_type is a type. For the string specialization, for example, value_type is char.

size_type is used like size_of, except that it returns the size of a string in terms of the stored type. For the string specialization, that would be in terms of char, in which case size_type is the same as size_of. It is an unsigned type.

difference_type is used to measure the distance between two elements of a string, again in units corresponding to the size of a single element. Typically, it would be a signed version of the type underlying size_type.

For the char specialization, pointer is type char *, and reference is type char &. However, if you create a specialization for a type of your own design, these types (pointer and reference) could refer to classes that have the same properties as the more basic pointers and references.

To allow Standard Template Library (STL) algorithms to be used with strings, the template defines some iterator types:

```
typedef (models random access iterator) iterator;
typedef (models random access iterator) const_iterator;
typedef std::reverse_iterator<iterator> reverse_iterator;
typedef std::reverse_iterator<const_iterator> const_reverse_iterator;
```