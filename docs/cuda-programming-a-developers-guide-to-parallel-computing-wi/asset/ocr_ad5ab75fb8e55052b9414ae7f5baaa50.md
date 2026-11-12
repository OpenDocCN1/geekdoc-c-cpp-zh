pointer. For the code to work correctly, the free() function also needs to handle null pointers. Thus, the start of the free function might be

```
if (ptr == NULL)
{
    ... search list of allocated memory areas for ptr and de-allocate memory.
}
```

The free() function needs to consider both receiving a null pointer and also an apparently valid pointer. The NULL pointer, however, doesn't point to a valid area of allocated memory. Typically, if you call free() with a null or an invalid pointer, a function that is written defensively will not corrupt the heap storage, but will instead do nothing. Defensive programming is about doing nothing erroneous in the case of bad inputs to a function.

However, this has a rather nasty side effect. While the user no longer sees the program crash, neither does the test or quality assurance department, or the author for that matter. In fact, the program now silently fails, despite programming errors in the caller. If a function has implicit requirements on the bounds or range of an input, this should be checked. For example, if a parameter is an index into an array, you should absolutely check this value to ensure the array access does not generate an out-of-bounds access. This is a question that is often addressed incorrectly.

C provides a very useful construct that is rarely used, except by those programmers familiar with good software engineering practices—the assert directive. When a program fails, to have it fail silently is bad practice. It allows bugs to remain in the code and go undetected. The idea behind assert is the opposite. If there is an error with the parameters passed by the caller, there is a programming error. The called function should scream about the issue until it's fixed. Thus, if a null pointer is not allowed as one of the input parameters to the function, then replace the if ptr != NULL check with the following:

```
// Null pointers not supported
assert(ptr_param != NULL);
```

This means we no longer require an additional indent, plus we document in the code the precondition for entry into the function. Always make sure you place a comment above the assertion explaining why the assertion is necessary. It will likely fail at some point in the future and you want the caller of that function to understand as quickly as possible why their call to the function is invalid. That caller may very often be yourself, so it's in your own best interests to ensure it is commented.

Six months from now you'll have forgotten why this precaution was necessary. You will then have to search around trying to remember why it was needed. It also helps prevent future programmers from removing the "incorrect" assertion and therefore making the problem "go away" before the upcoming release. Never do this without entirely understanding why the assertion was put there in the first place. In almost all cases, removing the assert check will simply mask an error later in the program.

When using assertions, be careful not to mix handling of programming errors with valid failure conditions. For example, this following code is incorrect:

```
char * ptr = malloc(1024);
assert(ptr == NULL);
```

It is a valid condition for malloc to return a NULL pointer. It does so when the heap space is exhausted. This is something the programmer should have a valid error handling case for, as it's