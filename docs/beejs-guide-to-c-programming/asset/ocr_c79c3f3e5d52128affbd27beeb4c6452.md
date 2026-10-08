# Chapter 18. The Outside Environment

```
arg 0: ./foo
arg 1: i
arg 2: Like
arg 3: turtles
```

It's a little weird, because the zeroth argument is the name of the executable, itself. But that's just something
to get used. The arguments themselves follow directly.

Source:

```
#include <stdio.h>

int main(int argc, char *argv[]) {

    for (int i = 0; i < argc; i++) {
        printf("%d %s\n", i, argv[i]);
    }
}
```

Whoa! What is going on the main() function signature? What's argc and argv² (pronounced arg-cee
and argv-wee)?

Let's start with the easy one: argc. It is the argument count, including the program name, itself.
If you think of all as an array of strings, which is exactly what they are, then you can think of
argc as the length of that array, which is exactly what it is.

And so we're doing in that loop is going through all the argvs and printing them out one at a time, so
for a given:

```
./foo i like turtles

arg 0: ./foo
arg 1: i
arg 2: like
arg 3: turtles
```

With that in mind, we should be good to go with our adder program.

Our plan:

+   * Look at all the command line arguments (past argv[0], the program name)
* Convert them to integers
* Add them to a running total
* Print the result

Let's get to it!

```
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char **argv) {
    int total = 0;

    for (int i = 1; i < argc; i++) { // Start at 1, the first argument
        int value = atoi(argv[i]); // Use strconv for better error handling
```

> Since they're just regular parameter names, you don't actually have to call them argc and argv. But it's so very idiomatic to use those names, if you get creative, other C programmers will look at you with a suspicious eye, indeed!