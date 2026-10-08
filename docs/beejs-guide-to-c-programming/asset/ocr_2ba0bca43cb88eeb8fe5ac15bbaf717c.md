# Chapter 29. Signal Handling

+   - SIG_IGN to ignore the signal.
- SIG_DFL to restore the default handler for the signal.

Let's write a program that you can CTRL-C out of. (Don't fret—in the following program, you can also hit RETURN and it'll exit.)

```
#include <stdio.h>
#include <signal.h>

int main(void)
{
    char s[1024];

    signal(SIGINT, SIG_IGN); // Ignore SIGINT, caused by ^C
    printf("Try hitting ^C... (hit RETURN to exit)\n");

    // Wait for a line of input so the program doesn't just exit
    fgets(s, sizeof s, stdin);
}
```

Check out line 8—we tell the program to ignore SIGINT, the interrupt signal that's raised when CTRL-C is hit. No matter much you hit it, the signal remains ignored. If you comment out line 8, you'll see you can CTRL-C with impunity and quit the program on the spot.

# 29.3 Writing Signal Handlers

I mentioned you could also write a handler function that gets called when the signal is raised.
These are pretty straightforward, are also capability-limited when it comes to the spec.

Before we, let's look at the function prototype for the signal(int):

```
void (*)(int sig, void (*func)(int))(int);
```

Pretty easy to read, right?
WRONG! :

Let's take a moment to it apart for practice.
signal() takes two arguments: an integer representing the signal, and a pointer func to the handler (the handler returns void and takes an int as an argument), highlighted below:

```
sig           func
|---|---|
void (*)(int sig, void (*func)(int))(int);
```

Basically, we're going to pass in the signal number we're interested in catching, and we're going to pass a pointer to a function of the form:

```
void f(int x);

```

will do the actual catching.
Now—what about the rest of that prototype for? It's basically all the return type. See, signal() will return whatever you passed as func on success... so means it's returning a pointer to a function that returns void and takes an int as an argument.

returned
function          indicates we're