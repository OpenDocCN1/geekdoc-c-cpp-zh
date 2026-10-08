
- The helpful and knowledgeable folks on r/C_Programming

# Chapter 41

## Function Specifiers, Alignment Specifiers/Operators

We don't see a heck of a lot of use in my experience, but we'll cover them here for the sake of completeness.

## 41.1 Function Specifiers

When you declare a function, you can give the compiler a couple tips about how the functions call or would be used. This enables or encourages the compiler to make certain optimizations.

### 41.1.1 inline for Speed—Maybe

You can declare a function to be inline like this:

```c
static inline int add(int x, int y) {
    return x + y;
}
```

This is meant to encourage the compiler to make this function call as fast as possible. And, historically, one way to do this is inlining, which means that the body of the function would be embedded in its entirety where the call was made. This would avoid all the overhead of setting up the function call and tearing it at the expense of larger code size as the function was copied all over the place instead of being reused.

That would seem to be the end of the story, but it's not. inline comes with a whole pile of rules that make for interesting times. I'm not sure I understand them all, and behavior seems to vary from compiler to compiler.

The short answer is define the inline function as static in the file that you need it. And then use it in one file. And you never have to worry about the rest of it.

But if you're wondering, here are more fun. Let's try leaving the static off.

```c
#include <stdio.h>

inline int add(int x, int y) {
    return x + y;
}
```

```c
int main(void)
{
    printf("%d\n", add(1, 2));
}
```

gcc gives a linker error on add()... unless you compile with optimizations (probably!)
See, a compiler can choose to inline or not, but if it chooses to, it will use no function at all. gcc doesn't inline unless you've defined an optimized build.

One way around this is to define a non-inline external linkage version of the function elsewhere, and that will be used when the inline one isn't. But as the programmer can't determine which, perhaps. If both are available, its unspecified which one the compiler chooses. With gcc the inline function will be used if you're compiling with optimizations, and the non-inline one will be used otherwise. If the bodies of these functions are created by...

Another way is to declare the function as extern inline. Then it will attempt to inline in this file, but also create a version with external linkage. And so gcc will use one or the other depending on optimizations, but at least they're the same function.

Unless, of course, you have another source file with an inline function of the same name; it will use the inline function or the one with external linkage depending on optimizations.

But let's say you're doing a build where the compiler is inlining the function. In that case, you can just use a plain inline. However, there are now restrictions.

You can refer to any statics:

```c
static int b = 13;
inline int add(int x, int y) {
    return x + y + b; // BAD -- can't refer to b
}
```

And you can define any non-const variables:

```c
int b = 13;
inline int add(int x, int y) {
    return x + y + b; // BAD -- can't define static
}
```

But making it const:

```c
static const int b = 13;
inline int add(int x, int y) {
    return x + y + b; // OK -- static const
}
```

Now, you know functions are external by default, so you should be able to call add() from another file. You'd like to think that, but you can't! If it's just a plain inline, it's only visible in that file. Okay, what if you throw an error there? Now we're coming full circle to what we discussed having inline mixed with external linkage. If both are visible, the compiler can choose which to use. Here's foo.c with the inline:

```c
// foo.c
#include <stdio.h>

inline char *func(void) {
    return "foo's function";
}

int main(void) {
    printf("%s\n", func());
    bar();
}
```

Recall that unless we're using an optimized build with gcc, func() will vanish and we'll get a linker error. Unless we have a version with external linkage defined in bar.c.

```c
// bar.c
#include <stdio.h>

char *func(void) {
    return "bar's function";
}

void bar(void) {
    printf("%s\n", func());
}
```

So the question is, what is the output? Seems like when we call func() from foo.c, it should print 'foo's function'. And from bar.c, it should print 'bar's function'. And if I compile with gcc with optimizations¹, it will use inline and we'll get the expected:

```
foo.c: foo's function
bar.c: bar's function
```

Great! But if we compile in gcc without optimizations, it ignores the inline function and uses the external linkage func() from bar.c! And we get this:

```
foo.c: bar's function
bar.c: bar's function
```
¹You can do this with -O on the command line.

In short, the rules are surprisingly complex. I give myself 30% chance of having described them correctly.

### 41.1.2 nooreturn and _noreturn

This indicates to the compiler that a particular function will never return to its caller, i.e. the program will exit by some mechanism before the function returns. It allows the compiler to perform some optimizations around the function call. It also allows you to indicate to devs that some program logic depends on a function returning. You'll likely need to use this, but you'll see it in some library calls exit² and everyone would recommend including <stdnoreturn.h> and using the easier-to-read nooreturn instead.

It's undefined behavior if a function specified as nooreturn actually does return. It's computationally costly, see. Here's an example of using nooreturn correctly:

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdnoreturn.h>

noreturn void foo(void) // This function should never return!
{
    printf("Happy days\n");
    exit(1); // And it doesn't return--it exits here!
}

int main(void) {
    foo();
}
```

If the compiler detects a nooreturn function could return, it might warn you, helpfully. Replacing the foo() function with this:

```c
noreturn void foo(void) {
    printf("Breakin' the law\n");
}
```

gets me a warning:
`foo.c:7:1: warning: function declared 'noreoreturn' should not return`

## 41.2 Alignment Specifiers and Operators

Alignment is all about multiples of addresses on which objects can be stored. You can store this at any address? Or it must be a starting address that's divisible by 2? Or 8?

If you're coding something low-level like a memory allocator that interfaces with your OS, you might need to consider this. Most devs go their careers without using this functionality in C.

### 41.2.1 aligns and Aligns

This isn't a function. Rather, it's an alignment specifier that you can use with a variable declaration. The built-in is _Align, the header <stdalign.h> defines it as aligns for something better. If you need your char to be aligned like an int, you can force it like this:

```c
char aligns(int) c;
```

You can also pass a constant value or expression for the alignment. This has to be supported by the system. Small powers of 2 (1, 2, 4, 8, and 16) are generally safe bets.

```c
char aligns(8) c; // align on 8-byte boundaries
```

If you want to align at the maximum alignment used by your system, include <stddef.h> and use the type max_align_t, like so:

```c
char aligns(max_align_t) c;
```

You could potentially over-align by specifying an alignment not than that of max_align_t, but whether or not such things are aligned is system dependent.

### 41.2.2 alignof and Alignof

This operator will return the address multiple a particular type uses for alignment on this system. For example, maybe chars are aligned every 1 address, and ints are aligned every 4 addresses. The built-in operator is _Alignof, the header <stdalign.h> defines it as alignof if you want to look cooler. Here's a program that will print out the alignment of a variety of different types. Again, these will vary from system to system. Note that the type max_align_t will give you the maximum alignment used by the system.

```c
#include <stdalign.h>
#include <stdio.h> // for printf(void)
#include <stddef.h> // for max_align_t

struct t {
  int a;
  char b;
  float c;
}

int main(void) {
  printf("char" : %u\n", alignof(char));
  printf("short" : %u\n", alignof(short));
  printf("int" : %u\n", alignof(int));
  printf("long" : %u\n", alignof(long));
  printf("long long" : %u\n", alignof(long long));
  printf("double" : %u\n", alignof(double));
  printf("long double" : %u\n", alignof(long double));
}
```
