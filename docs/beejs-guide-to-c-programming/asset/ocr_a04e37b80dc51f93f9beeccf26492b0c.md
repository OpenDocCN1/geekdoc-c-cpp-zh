# Chapter 17. Multiple Projects

}
See how from main() call add()but add() is in a completely different source file! It's in bar.c,
while the call to it is in foo.c!

If we build this with:

```
gcc -o foo foo.bar bar.c
```

error: implicit declaration of function 'add' is invalid in C99
(Or you might get a warning. Which you should not ignore. Never ignore warnings in C; address them all.)
If you recall the section on prototypes, implicit declarations are banned in modern C and there's
legitimate reason to introduce them into new code. We should fix it.
What implicit declaration means that we're using a function, add() in this case, without
letting C know anything about it ahead of time. C wants to know what it returns, what types it takes
arguments and such things as that.

We saw how to that earlier with a function prototype. Indeed, if we add one of foo.c before
make the call, everything works well:

```
// File foo.c

#include <stdio.h>

int add(int,int); // Add the prototype

int main(void)
{
    printf("%d\n", add(2, 3)); // 5!
}
```

No more error!
But that's a pain—needing to type in a prototype every time you want to use a function. I mean we used
printf() right there and didn't need to type in a prototype; what gives?
If you remember from back with back hello.c at the beginning of the book, we actually did include the
prototype for printf() It's in the file std.h! And we included that with #include
Can we do this with our add() function? Make a prototype for it and put it in a header file?
Sure!

Header files in C have a .h extension by default. And they often, but not always, have the same name as
the corresponding .c file. So let's make a bar.h for our bar.c file and we'll stick the prototype in it:

```
// File bar.h

int add(int,int);

Now let's modify foo.c to include that file. Assuming it's in the same directory, we include it inside
double quotes (as opposed to angle brackets):
```

```
// File foo.c

#include <stdio.h>

#include "bar.h" // Include from current directory
```