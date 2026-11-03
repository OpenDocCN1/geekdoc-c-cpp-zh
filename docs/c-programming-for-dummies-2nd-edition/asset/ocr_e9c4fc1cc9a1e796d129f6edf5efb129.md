Follow the typedef keyword with an existing C data type, data_type, and then the synonym for the data type, new_type. Use the same rules for naming a variable as you would for the new_type definition.

+   >> One advantage of using typedef with a structure is that it saves you from typing the word struct too many times.
+   >> Just about any data type you encounter in the C library other than a keyword, such as time_t, size_t, or st_mode, is most likely a typedef, declared in a header file. The library documentation (man page) explains the underlying data type, but you should use the typedef-defined name in your code to declare any required variables. For example:
+   >> The rare times the underlying data type for a typedef must be known is when using a typedef variable in a printf() statement. The conversion character must match the actual data type. Fortunately, modern compilers, like clang, report the correct conversion character to use.
+   >> Where programmers get into trouble with typedef and structures is when creating a linked list. I repeat this warning in Chapter 20, which covers linked lists.

```
time_t now;
```

The preceding statement creates a variable now of the time_t data type, defined in the time.h header file. See Chapter 21 for more information on C library time functions.

![](bbox=[0.15, 0.55, 0.22, 0.68])

# Making static variables

Variables used within a function are local to that function: Their values are used and then discarded when the function is done. Listing 16-5 demonstrates the concept.

# LISTING 16-5: Don't Give Me No static

```
#include <stdio.h>

void proc(void);

int main()
{
    puts("First call");
    proc();
    puts("Second call");
```