
```c
int x = 2;                         /* Global variable */
int main(void)
{
    int y = 22;                    /* Local variable of main */
    {
        int z = 222;               /* Local variable of block */
        /* x, y and z visible here */
    }                               /* End of block */
    /* x and y visible here, but not z */
}

int func(void)
{
    int p = 5;                      /* Local variable of func */
    /* x and p visible here, but not y and z */
}
```

**FIGURE II.4** Scope of Global and Local Variables

### 11.16.3 Variable Hiding

If an inner block re-declares a variable, then its new value *hides* both the global value and the old value assigned in the outer block (Fig. 11.5). A variable can be hidden by creating another one having the same name in memory. Hiding doesn’t overwrite the previous value, which becomes visible when the inner block is exited.

```c
int x = 2;                         /* Global variable */
int main(void)
{
    int y = 22;                    /* Local variable of main */
    {
        /* x and y visible here but only until they are re-declared */
        int x = 4;                 /* Hides the value 2 */
        int y = 44;                /* Hides the value 22 */
        int z = 88;                /* Nothing to hide */
    }
    /* Original values of x and y visible here, but z is undefined */
}
```

**FIGURE 11.5** Re-Defining Variables

The inner block this time re-declares (or re-defines) two variables, x and y. When the inner block is exited, none of the values that were seen inside the block are seen outside it. The old values of x and y become visible once more.

> **Takeaway:** A local or global variable ceases to be visible in an inner block if that block also declares a variable with the same name. However, the original variable becomes visible when the block is exited.

## 11.17 THE STORAGE CLASSES

The scope, lifetime and initial value of a variable are determined by its *storage class*. So far, we have used the default storage class for variables (automatic), but you also need to know the following storage classes supported by C:

- automatic (**auto**)
- static (**static**)
- external (**extern**)
- register (**register**)

The storage class also determines the way the compiler allocates memory for a variable. The keywords shown in parentheses are mutually exclusive, and only one of them can be used as a qualifier in a variable declaration. Table 11.1 makes a comparison of the key features of the four storage classes.

### 11.17.1 Automatic Variables (auto)

If a function is invoked repeatedly, its local variables are created and destroyed automatically as many times as the function is called. For this reason, local variables of a function are also known as *automatic variables*. The keyword **auto** used as a qualifier in a declaration makes a variable an automatic one. We have never used it though because, by default, a local variable has auto as its storage class. But we can also explicitly specify a variable as automatic:

```c
int main(void)
{
    auto short count = 0;
    count++;
    ...
}
```

*auto can be omitted*

*Always has the value 1*

An automatic variable has function scope and a junk default value. As seen above, you can’t use an automatic variable to count the number of times a function is called because every call initializes the variable to the same value. A global variable partially solves the problem since it is initialized once, but by depending on a variable that is defined outside **main**, a function loses its status as a self-contained unit. C has a simple solution to this problem which is discussed next.

> **Note:** Automatic variables are pushed onto the stack when the function is called and popped out after execution is complete (11.13.2—*Inset—How It Works*). For a variable to retain its value for the duration of the program, it must not be stored in the stack, i.e., it can’t have the **auto** storage class.

### 11.17.2 Static Variables (static)

If a local variable is assigned the *static* storage class, then it will retain its value between function calls. A static variable (keyword: **static**) is created and initialized just once, when the function containing its declaration is executed. It remains alive (is static) even after the function terminates.

This is how we declared a static variable in Section 11.13 to count the number of times the `main` function was called within `main`:

```c
static long count;                      Default value is zero
```

By default, a static variable is initialized to zero, but even if it is initialized explicitly, this is done just once. The following definition initializes `count` to 5 and increments it with every call made to the function:

```c
void f(void)
{
    static long count = 5;
    count++;                             count incremented with every call
}
```

For some reason, if you want a static variable to be initialized every time the function is called, then this is the way to do it:

```c
static long count;                      First initialized to zero ...
count = 5;                              ... and then assigned the value 5
```

The **static** qualifier can also be used with a global variable (defined before `main`), in which case the variable is accessible only in the current file. The static attribute doesn't affect the initialization property because a non-static global variable is initialized once anyway.

A function may also be declared as **static**, and that would make the function inaccessible in other files.

> **Takeaway:** A local variable of a function is created and extinguished every time the function is called and terminated. This default **auto** feature can be overridden with the **static** qualifier in which case the variable retains its value across multiple invocations of the function.

### 11.17.3 External Variables (extern)

A global or external variable is defined outside a function and is visible everywhere—even in other files that constitute the program. However, a variable declared after `main` is not visible in `main`:

```c
int main(void)
{
    ...
    return 0;
}                                       End of main
int x = 10;                             Not visible in main
```

To make matters worse, a variable declared at the end of the file is not visible anywhere—even in functions that are defined prior to the variable declaration. To make the variable visible at selected locations in the file, you need to assign the `extern` storage class to the variable. In the current scenario, for x to be visible in `main`, it must be declared there with the `extern` qualifier:

**TABLE 11.1** Storage Classes of Variables

| Storage Class | Visibility | Lifetime | Default Value | Remarks |
|---|---|---|---|---|
| `auto` | In function/block where declared | Duration of function/block | Junk | Default class for variable declared in function/block |
| `static` (in function) | In function/block where declared | Duration of program/block entry | Zero | Retains value between multiple function calls |
| `static` (outside function) | From point of declaration to end of file | Duration of program | Zero | Retains value across multiple files |
| `extern` | In function/block, file or multiple files | Duration of program | Zero | Must be declared at one place without `extern` |
| `register` | In function/block where declared | Duration of function/block | Junk | Stored in CPU register for faster access |

```c
int main(void)
{
    extern int x;
    ...
    return 0;
}
int x = 10;
```

*x declared here ...*

*... and defined here*

The **extern** keyword indicates that the variable x is merely *declared here* and that the *definition* has been made elsewhere (here, after **main**). This means storage for x is allocated only when it is defined, and the **extern** statement simply intimates type information to the compiler. *There is only one variable x here using a single storage location.* Without **extern**, x would be a local variable of **main** and would have no relation with the one that is defined later.

![](img/d75612dcf3ab36327142238ab5bb21d8_391_0.png)

> **Takeaway:** If a variable x is not visible in a function or a block, use the **extern** qualifier to make it visible there. Also, while a regular variable is declared and defined simultaneously, an extern variable can only be declared. It must be defined “elsewhere.”

### 11.17.4 `extern.c`: Using extern to Control Variable Visibility

Program 11.12 explores the visibility of two variables (x and y) and an array (arr) which are defined after **main**. x and arr are visible in **main** because of **extern**, but y is not. The y in **main** is an uninitialized automatic variable that doesn’t share storage with the y defined after **main**. Note that x declared in the block is by default not visible after the block is exited, the reason why it had to be re-declared with **extern**.
