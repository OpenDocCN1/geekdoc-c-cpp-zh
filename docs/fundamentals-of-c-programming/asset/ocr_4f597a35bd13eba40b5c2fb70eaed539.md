before t. The function returns an integer greater than zero if s appears lexicographically after t. The function returns zero if the two strings are identical.

The following code fragment

```
std::cout << strcmp("ABC", "XYZ") << '\n';
std::cout << strcmp("XYZ", "ABC") << '\n';
std::cout << strcmp("ABC", "ABC") << '\n';
```

prints:

```
-1
1
0
```

+   int strncmp(const char *s, const char *t, int n) compares the first n characters of two strings for lexicographic (dictionary) ordering. The function returns an integer less than zero if the first n characters of s appear lexicographically before the first n characters of t; that is, s would appear before t is a dictionary. The function returns an integer greater than zero if the first n characters of s appear lexicographically after the first n characters of t. The function returns zero if the first n characters of the two strings are identical.

You should be familiar with C strings because C++ code can use C libraries, and C libraries often use C strings. Since C strings tend to be problematic, however, in most cases you should use the newer string objects (see Section 13.1) whenever possible.

# 11.2.7 Command-line Arguments

Some programs executed from the command line accept additional arguments. For example, in a Microsoft Windows command prompt the command

```
copy count.cpp count2.cpp
```

makes a copy of a file. The macOS and Linux equivalent would be

```
cp count.cpp count2.cpp
```

These filenames are called command-line arguments. They are provided in addition to the program's name. Command-line arguments allow the user to customize in some way the behavior of the program when launching it. In the example above, the user specifies which file to copy and the name of its copy. C++ programs that process command-line arguments do so via an array.

Listing 11.22 (cmdlineargs.cpp) is a program meant to be executed from the command line with extra arguments. It simply reports the extra information the user supplied.

# Listing 11.22: cmdlineargs.cpp

```
#include <iostream>

int main(int argc, char *argv[]) {
    for (int i = 0; i < argc; i++)
        std::cout << "[" << argv[i] << "]\n";
}
```