to going to the very end of a loop.

# Section 10.2.6 Headers 253

# 10.2.6 Headers

The calculator uses standard-library facilities. Therefore, appropriate headers must be #include dto complete the program:

```
#include<iostream> // I/O
#include<string> // strings
#include<map> // map
#include<cctype> // isalpha(), etc.
```

All of these headers provide facilities in the std namespace, so to use the names they provide we must either use explicit qualification with std:: or bring the names into the global namespace by

```
using namespace std;
```

To avoid confusing the discussion of expressions with modularity issues, I did the latter. Chapter 14 and Chapter 15 discuss ways of organizing this calculator into modules using namespaces and how to organize it into source files.

# 10.2.7 Command-Line Arguments

After the program was written and tested, I found it a bother to first start the program, then type the expressions, and finally quit. My most common use was to evaluate a single expression. If that expression could be presented as a command-line argument, a few keystrokes could be avoided.

A program starts by calling main() (§2.2.1, §15.4). When this is done, main() is given two arguments specifying the number of arguments, conventionally called argc, and an array of arguments, conventionally called argv. The arguments are C-style character strings (§2.2.5, §7.3), so the type of argv is char*[argc+1]. The name of the program (as it occurs on the command line) is passed as argv[0], so argc is always at least 1. The list of arguments is zero-terminated; that is, argv[argc]==0. For example, for the command

```
dc 150/1.1934
```

the arguments have these values:

```
argc: 2 argv: 0
"dc" "150/1.1934"
```

Because the conventions for calling main() are shared with C, C-style arrays and strings are used. The idea is to read from the command string in the same way that we read from the input stream. A stream that reads from a string is unsurprisingly called an

istringstream (§38.2.2). So to calculate expressions presented on the command line, we simply have to get our Token_stream to read from an appropriate istream: