Within main(), the values on the original command-line can now be accessed and used like any other variable. We'll see shortly that we can also pass file names to main() from the command-line and open and access the contents of the files. The program below simply echoes its command-line arguments to the terminal window:

```
// echo1.c

#include <stdio.h>

int main(int argc, char *argv[]) {
    int i;

    for(i = 1; i < argc; i++) {
        printf("%s ", argv[i]);
    }
    printf("\n");

    return 0;
}
```

Since argv is a pointer to an array of pointers, we can rewrite the above program without using array indexing:

```
// echo2.c

#include <stdio.h>

int main(int argc, char *argv[]) {
    while(--argc > 0) {
        printf("%s ", *++argv);
    }
    printf("\n");
}
```

Since argv is a pointer to the beginning of the array of argument strings, incrementing it by 1, ++argv, makes it point at argv[1] instead of argv[0]. Each successive iteration moves it along to the next argument. *argv is then the pointer to that argument. When argc becomes 0, there are no arguments left.