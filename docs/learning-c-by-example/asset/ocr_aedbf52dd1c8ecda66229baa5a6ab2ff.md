# 3.3 Pointer

A pointer is a programming language object, whose value refers to (or “points to”) another value stored elsewhere in the computer memory using its address. A pointer references a location in memory, and obtaining the value stored at that location is known as dereferencing the pointer (source: http://en.wikipedia.org/wiki/Pointer_(computer_programming).

To obtain memory address of a variable, we can use & syntax. For instance, create a file, called **address.c**, and write this code.

```
```c
#include <stdio.h>

int main(int argc, const char* argv[]) {

    int n;
    n = 10;

    printf("value n: %d \n", n);
    printf("address n: %x \n", &n);

    return 0;
}
```
```

Save this file. Then, try to compile and run.

```
```bash
$ gcc -o address address.c
$ ./address
```
```

If success, we obtain memory address of variable n. A sample output of program can be seen in Figure below.