changes affect functions in other files (with the exception that a pointer to that function is passed to a function of another file). Also, you don't have to worry if the names you choose are used in other files as well, because even if it happens, there will be no conflict. Since the linkage is internal, the same names can be reused in other files. Here is a last example that puts these concepts together. Suppose that this program consists of two files. Both files must be compiled and linked together to get the complete program. You'll see how to do it in Chapter 17. Could you tell us what does it output?

```
/* First file. */
#include <stdio.h>
void test(void);
int ext = 10;
static int st = 20;
int main(void)
{
    test();
    printf("%d %d\n", ext, st);
    return 0;
}
```

```
/* Second file. */
#include <stdio.h>
extern int ext;
static int st;
void test(void)
{
    st++;
    printf("%d %d\n", ext, st);
    ext = 30;
}
```

Since the st variable is declared as static in the first file, it does not conflict with the st declared in the second file (either if this second st is declared as static or not). Notice that the definition of test() resides in the second file. Since st is initialized to 0 by default, test() outputs 10 and 1. Since test() changed the value of ext to 30, the program outputs 30 and 20.

# One-Dimensional Array as Argument

When a parameter of a function is a one-dimensional array, we write the name of the array followed by a pair of brackets. The length of the array can be omitted; in fact, this is the common practice. We'll explain later why. For example:

```
void test(int arr[]);
```