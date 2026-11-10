# **TABLE 11.1** Storage Classes of Variables

| Storage Class | Visibility | Lifetime | Default Value | Remarks |
|---|---|---|---|---|
| `auto` | In function/block where declared | Duration of function/block | Junk | Default class for variable declared in function/block |
| `static` (in function) | In function/block where declared | Duration of program/block entry | Zero | Retains value between multiple function calls |
| `static` (outside function) | From point of declaration to end of file | Duration of program | Zero | Retains value across multiple files |
| `extern` | In function/block, file or multiple files | Duration of program | Zero | Must be declared at one place without `extern` |
| `register` | In function/block where declared | Duration of function/block | Junk | Stored in CPU register for faster access |

```
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
```

The **extern** keyword indicates that the variable x is merely *declared here* and that the *definition* has been made elsewhere (here, after **main**). This means storage for x is allocated only when it is defined, and the **extern** statement simply intimates type information to the compiler. *There is only one variable x here using a single storage location.* Without **extern**, x would be a local variable of **main** and would have no relation with the one that is defined later.

![](bbox=[0.092, 0.707, 0.15, 0.744])

> **Takeaway:** If a variable x is not visible in a function or a block, use the **extern** qualifier to make it visible there. Also, while a regular variable is declared and defined simultaneously, an extern variable can only be declared. It must be defined “elsewhere.”

# 11.17.4  `extern.c`: Using extern to Control Variable Visibility

Program 11.12 explores the visibility of two variables (x and y) and an array (arr) which are defined after **main**. x and arr are visible in **main** because of **extern**, but y is not. The y in **main** is an uninitialized automatic variable that doesn’t share storage with the y defined after **main**. Note that x declared in the block is by default not visible after the block is exited, the reason why it had to be re-declared with **extern**.