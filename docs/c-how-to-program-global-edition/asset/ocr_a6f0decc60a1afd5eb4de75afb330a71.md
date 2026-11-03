# ### E.8.8 Return Without Expression

[This section can be read after Section 5.5.]

C99 adds tighter restrictions on returning from functions. In functions that return a non-void value, we are no longer permitted to use the statement

```
```c
return;
```
```

In compilers prior to C99 this is allowed but results in *undefined behavior* if the caller tries to use the returned value of the function. Similarly, in functions that do not return a value, we are no longer permitted to return a value. Statements such as:

```
```c
void returnInt() {return 1;}
```
```

are no longer allowed. C99 requires that compatible compilers produce warning messages or compilation errors in each of the preceding cases. [For more information, see C99 Standard Section 6.8.6.4.]

# ### E.8.9 `__func__` Predefined Identifier

[This section can be read after Section 13.9.]

The `__func__` predefined identifier is similar to the `__FILE__` and `__LINE__` preprocessor macros—it’s a string that holds the *name of the current function*. Unlike `__FILE__`, it’s not a string literal but a real variable, so it cannot be concatenated with other literals. This is because string literal concatenation is performed during preprocessing, and the preprocessor has no knowledge of the semantics of the C language proper.

# ### E.8.10 `va_copy` Macro

[This section can be read after Section 14.3.]

Section 14.3 introduced the `<stdarg.h>` header and facilities for working with variable-length argument lists. C99 added the `va_copy` macro, which takes two `va_list` objects and copies its second argument into its first argument. This allows for multiple passes over a variable-length argument list without starting from the beginning each time.

# ## E.9 New Features in the C11 Standard

C11 refines and expands the capabilities of C. At the time of this writing, most C compilers that support C11 implement only a *subset* of the new features. In addition, various new features are considered *optional* by the C11 standard. Microsoft Visual C++ provides only partial support for features that were added in C99 and C11. Figure E.9 lists C compilers that have incorporated various C11 features.

| Compiler | URL |
| --- | --- |
| GNU GCC | https://gcc.gnu.org/gcc-4.9/ |
| Clang/LLVM | clang.llvm.org/docs/ReleaseNotes.html |
| IBM XL C | http://www.ibm.com/software/products/en/ccompfami |
| Pelles C | www.smorgasbordet.com/pellesc/ |

Fig. E.9 | C11-compliant compilers.