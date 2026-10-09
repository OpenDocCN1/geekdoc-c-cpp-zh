11.8.6. Write a function **concatenate** to append one null-terminated string to another. I’ve deliberately not told you the parameters or return type, this is a design question for you to solve. When you have come up with your own solution, take a look at the standard library functions `strcat` and `strcat_s` to see how others have solved this problem. Of course, you should use the library functions rather than write your own.

11.8.7. Write a function **search** which takes as input two `char*` strings. The first should be `phrase`, a phrase to search for, the second should be `text`, some text to scan through. It should return the number of times `phrase` appears in `text`. So `search("be", "to be or not to be")` should return "2".

# ## 11.9 Summary

Pointers are an essential tool for a C programmer, but aren’t so important to a C++ programmer. Nevertheless you must use pointers to some extent if you want to work with data of variable sizes or with long-lived data. By far the easiest way to use pointers is to use the `shared_ptr` class.

+   - Pointers, references, and `shared_ptr` can be used to achieve similar things.
- Use `vector` and `string` rather than arrays or `char *`.
- References are a bit safer than pointers, for example you can’t call `delete` on a reference and you `must` initialise reference variables. So pass by reference is preferred to pass by pointer.
- A `shared_ptr` is a bit slower than a reference or a pointer, but is really the only viable option for long-lived data if you want to avoid memory leaks.