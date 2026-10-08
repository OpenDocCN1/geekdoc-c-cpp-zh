The comparison function (**cmp**) used by **qsort()** and **bsearch()** must have the type

```
int (*cmp)(const void* p, const void* q);
```

That is, no type information is known to the sort function that simply “sees” its array as a sequence of bytes. The integer returned is

+   - Negative if *p* is considered less than *q*
- Zero if *p* is considered equal to *q*
- Positive if *p* is considered greater than *q*

Note that **exit()** and **abort()** do not invoke destructors. If you want destructors called for constructed automatic and static objects (§A.4.2), throw an exception.

For more standard library functions see K&R or some other reputable C language reference.

# B.12 Other libraries

Looking through the standard library facilities, you’ll undoubtedly have failed to find something you could use. Compared to the challenges faced by programmers and the number of libraries available in the world, the C++ standard library is minute. There are many libraries for

+   - Graphical user interfaces
- Advanced math
- Database access
- Networking
- XML
- Date and time
- File system manipulation
- 3D graphics
- Animation
- Etc.

However, such libraries are not part of the standard. You can find them by searching the web or by asking friends and colleagues. Please don’t get the idea that the only useful libraries are those that are part of the standard library.