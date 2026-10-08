# Chapter 19. The C Preprocessor

Oops! Since multiplication takes precedence, do we do the $4 \times 3 = 12$ first, and get $3 + 12 + 4 = 19$. Not what we were after.

So have to fix this to make it right.

This is so common that you should automatically do it every time you make a parameterized macro!

The fix is easy: just add some parentheses,

```
#define SQR(x) (x) // Better... still not quite good enough!
```

And now our macro expands to:

```
printf("%d%n", (3 + 4) * (3 + 4)); // 49! Woo woo!
```

But we will still have some problem which might happen if we have a higher-precedence operator than multiply (* ) nearby.

So the proper, way to put the macro is to wrap the thing in additional parentheses, like so:

```
#define SQR(x) ((x)) // Good!
```

Just make it a habit to do that when you make a math macro you can't go wrong.

# 19.5.2 Macros with One Argument

You can stack these things as much as you want:

```
#define TRIANGLE(a, w, h) (0.5 * (w) * (h))
```

Let's make some macros for $x$ using the quadratic formula. In case you don't have it on the top of your head, it says for equations of the:

```
ax^2 + bx + c = 0
```

you can solve for $x$ with the quadratic formula:

```
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
```

Which is crazy. Also the plus-or-minus ($\pm$) in there, indicating that there are actually two solutions.
Let's make some macros for:

```
#define QUADP(a, b, c) (((-(b) + sqrt((b) * (b) - 4 * (a) * (c)))) / (2 * (a)))
#define QUADM(a, b, c) (((-(b) - sqrt((b) * (b) - 4 * (a) * (c))) / (2 * (a)))
```

So that gets us some math. But let's define one more that we can use as arguments to printf() to print answers.

```
//
// replacement
// |------|-----------|-------
#define QUAD(a, b, c), QUADP(a, b, c), QUADM(a, b, c)
```

That's just some values separated by a comma—and we can use that as a "combined" argument of sorts to printf():

```
printf("x = %f or x = %f\n", QUAD(2, 10, 5));
```

Let's put it together some code:

```
#include <stdio.h>
#include <math.h> // For sqrt()
```