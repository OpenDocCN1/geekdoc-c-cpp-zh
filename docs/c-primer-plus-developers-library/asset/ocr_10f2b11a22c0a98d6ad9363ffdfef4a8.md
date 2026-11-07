```
cout << "Capacity after empty.reserve(50): "
     << empty.capacity() << endl;
return 0;
}
```

Here is the output of the program in Listing 16.4 for one C++ implementation:

```
Sizes:
    empty: 0
    small: 3
    larger: 34
Capacities:
    empty: 15
    small: 15
    larger: 47
Capacity after empty.reserve(50): 63
```

Note that this implementation uses a minimum capacity of 15 characters and seems to use 1 less than multiples of 16 as standard choices for capacities. Other implementations may make different choices.

What if you have a string object but need a C-style string? For example, you might want to open a file whose name is in a string object:

```
string filename;
cout << "Enter file name: ";
cin >> filename;
ofstream fout;
```

The bad news is that the open() method requires a C-style string argument. The good news is that the c_str() method returns a pointer to a C-style string that has the same contents as the invoking string object. So you can use this:

```
fout.open(filename.c_str());
```

# ## String Varieties

This section treats the string class as if it were based on the char type. In fact, as mentioned earlier, the string library really is based on a template class:

```
template<class charT, class traits = char _traits<charT>,
         class Allocator = allocator<charT> >
basic_string {...};
```

The basic_string template comes with four specializations, each of which has a typedef name:

```
typedef basic_string<char> string;
typedef basic_string<wchar_t> wstring;
typedef basic_string<char16_t> u16string;    // C++11
typedef basic_string<char32_t> u32string ;   // C++11
```