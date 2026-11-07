optimize performance. Chapter 18, “Visiting with the New C++ Standard,” discusses this topic in the section “Move Semantics and the rvalue Reference.”

The `string(initializer_list<char> il)` constructor enables list-initialization for the `string` class. That is, it makes declarations like the following possible:

```
```cpp
string piano_man = {'L', 'i', 's', 'z', 't'};
string comp_lang {'L', 'i', 's', 'p'};
```
```

This may not be that useful for the string class because using C-style strings is easier, but it does satisfy the intent to make the list-initialization syntax universal. This chapter will discuss the `initializer_list` template further later on.

# The string Class Input

Another useful thing to know about a class is what input options are available. For C-style strings, recall, you have three options:

```
```cpp
char info[100];
cin >> info;             // read a word
cin.getline(info, 100);  // read a line, discard \n
cin.get(info, 100);     // read a line, leave \n in queue
```
```

For string objects, recall, you have two options:

```
```cpp
string stuff;
cin >> stuff;             // read a word
getline(cin, stuff);      // read a line, discard \n
```
```

Both versions of `getline()` allow for an optional argument that specifies which character to use to delimit input:

```
```cpp
cin.getline(info,100,':');   // read up to :, discard :
getline(stuff, ':');          // read up to :, discard :
```
```

The main operational difference is that the string versions automatically size the target string object to hold the input characters:

```
```cpp
char fname[10];
string lname;
cin >> fname;       // could be a problem if input size > 9 characters
cin >> lname;       // can read a very, very long word
cin.getline(fname, 10);  // may truncate input
getline(cin, fname);     // no truncation
```
```

The automatic sizing feature allows the string version of `getline()` to dispense with the numeric parameter that limits the number of input characters to be read.

A design difference is that the C-style string input facilities are methods of the `istream` class, whereas the string versions are standalone functions. That’s why `cin` is an invoking object for C-style string input and a function argument for string object input. This applies to the `>>` form, too, which is evident if the code is written in function form: