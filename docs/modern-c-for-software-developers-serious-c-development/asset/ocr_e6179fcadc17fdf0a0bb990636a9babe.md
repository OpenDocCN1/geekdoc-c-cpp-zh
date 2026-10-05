```
void funbar(void);
```

# Step 3: Compile The Library Source Files

Compile the library source files and produce object files:

```
gcc -c foo.cpp -o foo.o
gcc -c bar.cpp -o bar.o
```

If we are creating a dynamic library, the library source files must be compiled with the -fPIC option. PIC is an acronym for position independent code:

```
gcc -fPIC -c foo.cpp -o foo.o
gcc -fPIC -c bar.cpp -o bar.o
```

# Step 4: Create The Static Library

Create the static library by bundling all of the object files into one static library:

```
ar rcsv some/path/libfoobar.a path/foo.o path/bar.o
```

ar is the gnu archive program. The options are: r - replace, c - create an archive, v - verbose, s - create an index. The paths to the object files are specified on the command line.

# Step 5: Link The Static Library Into A Program

We can use the library libfoobar.a as follows. Create a main program:

```
/* filename: driver.cpp */
#include "libfoobar.h"
void main()
{
    fun();
    bar();
}
```