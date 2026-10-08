+   • *Local scope*: A name is in a local scope if it is declared inside a function (this includes function parameters).
• *Class scope*: A name is in a class scope if it is the name of a member of a class.
• *Statement scope*: A name is in a statement scope if it is declared in the ( . . . ) part of a **for**-, **while**-, **switch**-, or **if**-statement.

The scope of a variable extends (only) to the end of the statement in which it is defined. For example:

```
for (int i = 0; i<v.size(); ++i) {
    // i can be used here
}
if (i < 27)         // the i from the for-statement is not in scope here
```

Class and namespace scopes have names, so that we can refer to a member from “elsewhere.” For example:

```
void f();            // in global scope

namespace N {
    void f()         // in namespace scope N
    {
        int v;       // in local scope
        ::f();       // call the global f()
    }
}

void f()
{
    N::f();          // call N's f()
}
```

What would happen if you called **N::f()** or **::f()**? See also §A.15.

# A.4.2  Storage class

There are three *storage classes* (§17.4):

+   • *Automatic storage*: Variables defined in functions (including function parameters) are placed in automatic storage (i.e., “on the stack”) unless explicitly declared to be **static**. Automatic storage is allocated when a function is called and deallocated when a call returns; thus, if a function is (directly