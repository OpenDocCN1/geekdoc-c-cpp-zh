# The string Class

optimize performance. Chapter 18, "Visiting with the New C++ Standard," discusses this topic in the section "Move Semantics and the rvalue Reference."

The string(initializer_list<char>) constructor enables-initialization of the string class. That is, it makes declarations like the following:

```
string piano_man = {'L', 'i', 'g', 'z', 't'};
string comp_lang = {'L', 'i', 's', 'p'};
```

This may not be useful for the string class because using C-style strings is easier, but it does satisfy the intent to make the list-initialization syntax universal.This chapter will discuss the initializer_list template later on.

# The string Class Input

Another useful thing to know about class is what inputs are available. For C-style strings, recall, you have three options:

```
char info[100]; // read a word
cin >> info;
cin.getline(info, 100); // read a line, discard 

cin.get(info, 100); // read a line, leave \n in queue
```

For string objects, recall, you have two options:

```
string stuff; // read a word
cin >> stuff;
getline(cin, stuff); // read a line, discard \n
```

Both versions of getline() allow for an optional argument that specifies which-character to delete input:

```
cin.getline(info, 100, ':'); // read up to :, discard :
getline(stuff, ':'); // read up to :, discard :
```

The main operational difference is that the string versions automatically size the-string object to hold the input characters:

```
char fname[10];
string fname;
cin >> fname; // could be a problem if input size > 9 characters
cin >> fname; // can read a ver, very long word
cin.getline(fname, 10); // may truncate input
getline(cin, fname); // no truncation
```

The automatic sizing feature allows the string version of getline() to dispense with the numeric parameter that limits the number of characters to be read.

A design difference is that the C-style string input facilities are methods of the istream class, whereas the string versions are standalone functions.That's why cin is an invoking object for C-style string input and a function argument for string object input. This applies to the >> form, too, which is evident if the code is written in function: