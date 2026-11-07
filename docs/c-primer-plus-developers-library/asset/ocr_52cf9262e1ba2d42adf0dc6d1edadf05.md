Here are a couple examples:

```
```cpp
string test("The");
test.append("ory");  // test is "Theory"
test.append(3, '!'); // test is "Theory!!!"
```
```

The operator+() function is overloaded to enable string concatenation. The overloaded functions don't modify a string; instead, they create a new string that consists of one string appended to a second. The addition functions are not member functions, and they allow you to add a string object to a string object, a string array to a string object, a string object to a string array, a character to a string object, and a string object to a character. Here are some examples:

```
```cpp
string s1("red");
string s2("rain");
string s3 = s1 + "uce";  // s3 is "reduce"
string s4 = 't' + s2;    // s4 is "train"
string s5 = s1 + s2;     // s5 is "redrain"
```
```

# ## More Assignment Methods

In addition to the basic assignment operator, the string class provides assign() methods, which allow you to assign a whole string or a part of a string or a sequence of identical characters to a string object. Here are the prototypes for the various assign() methods:

```
```cpp
basic_string& assign(const basic_string& str);
basic_string& assign(basic_string& str) noexcept;  // C++11
basic_string& assign(const basic_string& str, size_type pos,
                     size_type n);
basic_string& assign(const charT* s, size_type n);
basic_string& assign(const charT* s);
basic_string& assign(size_type n, charT c); // assign n copies of c
template<class InputIterator>
    basic_string& assign(InputIterator first, InputIterator last);
basic_string& assign(initializer_list<charT>);  // C++11
```
```

Here are a couple examples:

```
```cpp
string test;
string stuff("set tubs clones ducks");
test.assign(stuff, 1, 5);   // test is "et tu"
test.assign(6, '#');        // test is "######"
```
```