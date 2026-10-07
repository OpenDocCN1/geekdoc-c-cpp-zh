# 566 LESSON 22 Advanced Compiler Use

> CAUTION If you use extern declarations and then don't actually declare the variable elsewhere, you get an error. This error can occur either when you link the final program or at runtime.

FIGURE 22.5
Using the extern keyword to make an external variable visible across modules.

```
/* main module */
int x, y;
main() {
...
}
```

```
/* secondary mod1.c */
extern int x, y;
funcl() {
...
}
```

```
/* secondary mod2.c */
extern int x;
func4() {
...
}
```

In Figure 22.5, the variable x is visible throughout all three modules. In contrast, y is visible only in the main module and secondary module 1.

| DO | DON'T |
|---|---|
| DO create generic functions in their own source files. This way, they can be linked into any other programs that need them. | DON'T try to comiple multiple source files together if more than one module contains a main() function. You can have only one main(). (You can have only one function of any name.)
BDON'T always use the C source files when compiling multiple files together. If you compile a source file into an object file, recompile only when the file changes. This saves a great deal of time. |