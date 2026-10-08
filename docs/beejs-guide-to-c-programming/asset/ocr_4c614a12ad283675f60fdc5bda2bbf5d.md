which means you can do pointer arithmetic on argv.

So an alternate way to consume the command line arguments might be to just walk along the argv array by bumping a pointer until we hit NULL at the end.

Let's modify our <stdio.h>

```
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char **argv) {
    int total = 0;

    // Cute trick to get the compiler to stop warning about the
    // unused variable argc:
    (void)argc;

    for (char *p = argv + 1; *p != NULL; p++) {
        int value = atoi(*p); // Use strtol() for better error handling
        total += value;
    }

    printf("%d\n", total);
}
```

Personally use array notation to access argv, but have seen this floating around, as well.

# 18.1.3 Fun Facts

Just a few more things about argc and argv.

+   * Some environments might not set argv[0] to the program name. If it's not available, argv[0] will be an empty string. I've never seen this happen.
* The spec is actually pretty liberal with what an implementation can do with argv and where those values come from. But every system I've on works the same way, as we've discussed in this section.
* You can modify argc, argv, or any of the strings that argv points to. (Just don't make those strings longer than they are already!)
* On Unix-like systems, modifying the string argv[0] results in the output of ps changing.

Normally, if you have a program called foo that you run with ./foo, you might see this in the output of ps:

```
4079 tty1 S 0:00 /foo
```

If you modify(argv[0], "Hi") like so, because the new string "Hi!" is the same length as the old "./foo":

```
strcpy(argv[0], "Hi");

and then run the program ./foo it is still executing, we'll see this instead:
```

```
4079 tty1 S 0:00 Hi!
```

This behavior is not in the spec and is highly system-dependent.

> ^ps, Process Status, is a Unix command to see what processes are running at the moment.