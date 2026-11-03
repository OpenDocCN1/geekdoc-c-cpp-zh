# LISTING 11-5: (continued)

```
result = pow(value,3);
printf("%.2f to the 3rd power is %.2f\n", value,result);
result = floor(value);
printf("The floor of %.2f is %.2f\n", value,result);
result = ceil(value);
printf("And the ceiling of %.2f is %.2f\n", value,result);
return(0);
}
```

I've wrapped the long printf() statements in Listing 11-5 so that they fit on the page in this book. You need not wrap long statements in your own source code files.

# Exercise 11-11:

Type the source code from Listing 11-5 into your editor. Save. Build the project. Run it and try various values as input to peruse the results.

If you see any "undefined reference" errors from the linker at the Linux command prompt, add the -lm switch to the command-line compiling options, as described earlier in this chapter.

# Exercise 11-12:

Write a program that displays the powers of 2, from 2^9 through 2^10.

These are the Holy Numbers of Computing.

+   - The math functions listing in Table 11-3 are only a small sampling of the variety available.
+   - If your code requires some sort of mathematical operation, check the C library documentation, the man pages, to see whether that specific function exists.
+   - On a Unix system, type man 3 math to see a list of the C library's math functions.
+   - The ceil() function is pronounced "seal." It's from the word ceiling, which is a play on the floor() function.