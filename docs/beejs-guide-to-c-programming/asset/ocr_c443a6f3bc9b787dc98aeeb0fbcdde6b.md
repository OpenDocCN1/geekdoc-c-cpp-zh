# Chapter 18. The Outside Environment

$ ./foo
Value: C is awesome!

In this way, you can set up data environment variables, and you can get it in your C code and modify your behavior accordingly.

# 18.3.1 Setting Environment Variables

This isn't standard, but a list of systems provides ways to set environment variables.

If on a Unix-like, look up the documentation for putenv(), setenv(), and unsetenv(). On Windows, use _putenv().

# 18.3.2 Unix- Alternative Environment Variables

If you're on a Unix-like system, you have another couple ways of getting access to environment variables. Note that although the spec points this out as a common extension, it's not truly part of the C standard. It is, however, part of the POSIX standard.

One of these is a called environ that must be declared like so:

```
extern **environ;
```

It's an array of strings terminated with a NULL pointer.

You should declare yourself before you use it, or you might find it in the non-standard <unistd.h> header file.

Each string is in the form "key=value" so you'll have to split and parse it if you want to get the keys and values.

Here's an example of looping and printing out the environment variables couple different ways:

```
#include <stdio.h>

extern **environ; // MUST be extern AND named "environ"

int main(void)
{
    for (char **p = environ; *p != NULL; p++) {
        printf("%s\n", *p);
    }

    // Or you could do this:
    for (int i = 0; environ[i] != NULL; i++) {
        printf("%s\n", environ[i]);
    }
}
```

For a bunch of output that looks like this:

```
SHELL=/bin/bash
COLORTERM=true
TERM_PROGRAM_VERSION=1.53.2
LOGNAME=beej
HOME=/home/bee
et ...
```

Use getenv() if at all possible because it's more portable. But if you have to iterate over environment variables, using environ might be the way to go.