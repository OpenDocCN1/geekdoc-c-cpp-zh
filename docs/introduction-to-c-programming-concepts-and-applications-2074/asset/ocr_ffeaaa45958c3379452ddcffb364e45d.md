# void

A type indicating no information; commonly used to specify the return type for functions that do not need to return a value.

# while

Loop designator. The keyword is followed by a conditional in parentheses and then by commands to be executed repeatedly, as long as the conditional evaluates to true at the beginning of the loop.

Predefined commands are commonly used commands (e.g., as part of the C++ Standard Library) that are not actually part of the C++ language itself.

```
// PREDEFINED COMMANDS
```

begin

A member function of a container returning an iterator pointing
A member function of a container returning an iterator pointing to the first element in a container. Calling .begin() on the container will return the iterator.

# eof

Member function for finding whether you have encountered the
of of a file. Only when you have tried to read something past the end of the file will .eof() return true.

# cin

A source (obtained by using #include<iostream>) for
streaming console input (input typed in the user).

# failbit

A particular exception that is thrown when a file is opened
incorrectly.

# cout

A destination (obtained by using #include<iostream>) for
streaming console output (output to be printed in the console
window).

# find

An algorithm (obtained by using #include<algorithm>) for
performing a linear search through a container (such as an
ray or vector). It takes an iterator to a beginning and ending iterator
an element value to find. It returns an iterator to the
first position where a matching element is found or the ending
iterator is not found. Likewise, there is a .find() member
of the string class for finding a substring within string
(the substring is the only parameter, returning string::npos
nothing is found).

# end

A member function of a container returning an iterator pointing
to the position after the last element of a container.
Calling .end() will return the iterator. Typically, you use this by
incrementing the iterator until it reaches .end(), indicating that
you have reached the end of the container.