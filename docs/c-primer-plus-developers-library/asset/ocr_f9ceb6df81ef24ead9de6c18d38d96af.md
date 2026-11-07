The front() methods access the first element of a string, acting like operator[](). The back() methods access the last element of a string, acting like operator[](size() - 1).

# ## Basic Assignment

C++11 has five overloaded assignment methods, up two from C++98:

```
~~~cpp
basic_string& operator=(const basic_string& str);
basic_string& operator=(const char* s);
basic_string& operator=(char c);
basic_string& operator=(basic_string&& str) noexcept;   // C++11
basic_string& operator=(initializer_list<char>);        // C++11
~~~
```

The first assigns one string object to another, the second assigns a C-style string to a string object, the third assigns a single character to a string object, the fourth uses move semantics to assign an rvalue string object to a string object, and the fifth allows assignment of an initializer list. Thus, all the following operations are possible:

```
~~~cpp
string name("George Wash");
string pres, veep, source, join, awkward;
pres = name;
veep = "Road Runner";
source = 'X';
join = name + source;   // now with move semantics!
awkward = {'C','l','o','u','d','s','a','u','r'};
~~~
```

# ## String Searching

The string class provides six search functions, each with four prototypes. The following sections describe them briefly.

# ### The find() Family

Here are the find() prototypes as provided by C++11:

```
~~~cpp
size_type find (const basic_string& str, size_type pos = 0) const noexcept;
size_type find (const char* s, size_type pos = 0) const;
size_type find (const char* s, size_type pos, size_type n) const;
size_type find (charT c, size_type pos = 0) const noexcept;
~~~
```

The first member returns the beginning position of the str substring's first occurrence in the invoking object, with the search beginning at position pos. If the substring is not found, the method returns npos.

Here's code for finding the location of the substring "hat" in a longer string:

```
~~~cpp
string longer("That is a funny hat.");
string shorter("hat");
~~~
```