```
{
    total += 2*i*i + 1;
#ifdef JUST_CHECKING
    printf("i=%d, running total = %d\n", i, total);
#endif
}
    printf("Grand total = %d\n", total);

    return 0;
}
```

Compiling and running the program as shown produces this output:

```
i=1, running total = 3
i=2, running total = 12
i=3, running total = 31
i=4, running total = 64
Grand total = 64
```

If you omit the JUST_CHECKING definition (or enclose it inside a C comment, or use #undef to undefine it) and recompile the program, only the final line is displayed. You can use this approach, for example, to help in program debugging. Define JUST_CHECKING and use a judicious selection of #ifdefs, and the compiler will include program code for printing intermediate values for debugging. After everything is working, you can remove the definition and recompile. If, later, you find that you need the information again, you can reinsert the definition and avoid having to retype all the extra print statements. Another possibility is using #ifdef to select among alternative chunks of codes suited for different C implementations.

# The #ifndef Directive

The #ifndef directive can be used with #else and #endif in the same way that #ifdef is. The #ifndef asks whether the following identifier is not defined; #ifndef is the negative of #ifdef. This directive is often used to define a constant if it is not already defined. Here’s an example:

```
/* arrays.h */
#ifndef SIZE
#define SIZE 100
#endif
```

(Older implementations might not permit indenting the #define directive.)

Typically, this idiom is used to prevent multiple definitions of the same macro when you include several header files, each of which may contain a definition. In this case, the definition in the first header file included becomes the active definition and subsequent definitions in other header files are ignored.