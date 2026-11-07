Let’s look at how to create the three different kinds of static duration variables; then we can go on to examine their properties. To create a static duration variable with external linkage, you declare it outside any block. To create a static duration variable with internal linkage, you declare it outside any block and use the `static` storage class modifier. To create a static duration variable with no linkage, you declare it inside a block, using the `static` modifier. The following code fragment shows these three variations:

```
```c
...
int global = 1000;          // static duration, external linkage
static int one_file = 50;   // static duration, internal linkage
int main()
{
...
}
void funct1(int n)
{
    static int count = 0;   // static duration, no linkage
    int llama = 0;
...
}
void funct2(int q)
{
...
}
```
```

As stated previously, all the static duration variables (`global`, `one_file`, and `count`, in this example) persist from the time the program begins execution until it terminates. The variable `count`, which is declared inside `funct1()`, has local scope and no linkage, which means it can be used only inside the `funct1()` function, just like the automatic variable `llama`. But unlike `llama`, `count` remains in memory even when the `funct1()` function is not being executed. Both `global` and `one_file` have file scope, meaning they can be used from the point of declaration until the end of the file. In particular, both can be used in `main()`, `funct1()`, and `funct2()`. Because `one_file` has internal linkage, it can be used only in the file containing this code. Because `global` has external linkage, it also can be used in other files that are part of the program.

All static duration variables share the following initialization feature: An uninitialized static variable has all its bits set to 0. Such a variable is said to be *zero-initialized*.

Table 9.1 summarizes the storage class features as used in the pre-namespace era. Next, we’ll examine the static duration varieties in more detail.

Note that the keyword `static` has somewhat different meanings in the two uses shown in Table 9.1. When used with a local declaration to indicate a static variable with no linkage, `static` indicates the kind of storage duration. When used with a declaration outside of a block, `static` indicates internal linkage; the variable already has static duration. One might term this *keyword overloading*, with the precise meaning determined by context.