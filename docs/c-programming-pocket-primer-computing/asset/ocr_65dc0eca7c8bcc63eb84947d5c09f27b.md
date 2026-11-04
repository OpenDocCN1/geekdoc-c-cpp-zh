```
    char str3[] = "California";
    findChar(str3, 'z');

    return (0);
}
```

**Listing 7.22** contains a local header file called `FindChar2.h` (i.e., it's not part of the C language), followed by a `main()` function. Notice that the `main()` function defines three strings and invokes the `findChar()` function (defined in `FindChar2.c`) three times.

The C programs `FindChar2.c` and `FindMain2.c` need to be specified in the compilation step involving `gcc`, as shown here:

```
# do not change the order of the next two lines:
gcc -std=c11 -Wall -c FindChar2.c
gcc -std=c11 FindChar2.o FindMain2.c -o FindMain2
```

The output of the preceding code snippet is the binary executable `FindMain2`, and the output from launching `FindMain2` is here:

```
String: pasta
Char: a
Match in position: 1
Match in position: 4
Count: 2

String: New York City
Char: k
Match in position: 7
Count: 1

String: California
Char: z
```

The preceding example is manageable because there are only three files involved, which you can specify from the command line when you invoke `gcc`. However, a C