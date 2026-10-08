# Chapter 19. The C Preprocessor

| Macro | Description |
| _STDC_LIB_EXT1_ | 1 if this implementation supports a variety of “safe” alternate standard library functions (they have _s suffixes on the name) |
| _STDC_NO_ATOMICS_ | 1 if this implementation does not support _Atomic or <statomic.h> |
| _STDC_NO_COMPLEX_ | 1 if this implementation does not support complex types or <complex.h> |
| _STDC_NO_THREADS_ | 1 if this implementation does not support <threads.h> |
| _STDC_NO_VLA_ | 1 if this implementation does not support variable-length arrays |

# 19.5 Macros with Arguments

Macros are more powerful than simple substitution, though. You can set them up to take arguments that are substituted in, as well.

A question often arises for when to use macros versus functions. Short answer: use functions. But you’ll see lots of macros in the wild and in the standard library. People tend to use them for short, mathy things, and also for features that might change from platform to platform. You can define different keywords for one or the other.

# 19.5.1 Macros with One Argument

Let’s start with a simple one that squares a number:

```
#include <stdio.h>

#define SQR(x) x * x // Not quite right, but bear with me

int main(void)
{
    printf("%d\n", SQR(12)); // 144
}
```

What’s saying is “everywhere you see SQR with some value, replace it with that value times itself”.
So line 7 be changed to:

```
printf("%d\n", 12 * 12); // 144
```

Which C comfortably converts to 144.

We’ve made an elementary error in that, one that we need to avoid.

Let’s check it out. If we wanted to compute SQR(3 + 4)? Well, 3 + 4 = 7, so we must want to compute $7^2 = 49$. That’s 49—final answer.
Let’s drop it in our code and see what we get... 19!!

```
printf("%d\n", SQR(3 + 4)); // 19!!
```

What happened?
If we follow the macro expansion, we get

printf("%d\n", 3 + 4 * 3 + 4); // 19!