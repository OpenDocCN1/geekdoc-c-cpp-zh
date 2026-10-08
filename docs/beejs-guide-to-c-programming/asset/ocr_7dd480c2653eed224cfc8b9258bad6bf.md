# 28.1.3 Setting Up Exit Handlers with atexit()

You can register functions when a program exits whether by returning from main() or calling the exit() function.

A call to atexit() with the handler function name will get it done. You can register multiple exit handlers, and they'll be called in the reverse order of registration.

Here's an example:

```
#include <stdio.h>
#include <stdlib.h>
```

```
void on_exit_1(void)
{
    printf("Exit handler called!\n");
}

void on_exit_2(void)
{
    printf("Exit handler 2 called!\n");
}

int main(void)
{
    atexit(on_exit_1);
    atexit(on_exit_2);

    printf("About to exit...\n");
}
```

And the output is:

About to exit...
Exit handler 2 called!
Exit handler 1 called!

# 28.2 Quicker Exits with quick_exit()

This is similar to a normal exit, except:

+   * Open files might not be flushed.
* Temporary files might not be removed.
* atexit() handlers won't be called.

But there is a way to register exit handlers: call at_quick_exit() analogously to how you'd call atexit

```
#include <stdio.h>
#include <stdlib.h>
```

```
void on_quick_exit_1(void)
{
    printf("Quick exit handler 1 called!\n");
}
```

```
void on_quick_exit_2(void)
{
    printf("Quick exit handler 2 called!\n");
}
```