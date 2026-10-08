to the design of C++ was that the compiler could easily check much (but not all) of what lint checked.

You can ask to have function arguments checked in C. You do that simply by declaring a function with its argument types specified (just as in C++). Such a declaration is called a *function prototype*. However, beware of function declarations that do not specify arguments; those are *not* function prototypes and do not imply function argument checking:

```
int g(double);           /* prototype — like C++ function declaration */
int h();                /* not a prototype — the argument types are unspecified */

void my_fct()
{
    g(0);                    /* error: missing argument */
    g("asdf");              /* error: bad argument type */
    g(2);                    /* OK: 2 is converted to 2.0 */
    g(2,3);                  /* error: one argument too many */

    h(0);                    /* OK by the compiler! May give unexpected results */
    h("asdf");              /* OK by the compiler! May give unexpected results */
    h(2);                    /* OK by the compiler! May give unexpected results */
    h(2,3);                  /* OK by the compiler! May give unexpected results */
}
```

The declaration of **h()** specifies no argument type. This does not mean that **h()** doesn't accept arguments; it means "Accept any set of arguments and hope they are correct for the called function." Again, a good compiler warns and lint will catch the problem.

C++	C equivalent
void f( ); // preferred	void f(void);
void f(void);	void f(void);
void f( . . ); // accept any arguments	void f(); /* accept any arguments */

There is a special set of rules for converting arguments where no function prototype is in scope. For example, **char**s and **short**s are converted to **int**s, and **float**s are converted to **double**s. If you need to know, say, what happens to a **long**, look it up in a good C textbook. Our recommendation is simple: don't call functions without prototypes.