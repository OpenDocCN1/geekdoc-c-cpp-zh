| Attribute | Description |
| :--- | :--- |
| Type | char, int, unsigned int, etc. (_also implies size, range, and resolution_) |
| Name | The identifier used to access the object |
| Value | The data held within the object |
| Address | The location in memory where the object resides |
| Scope | That part of the source code where the object's name is recognized |
| Lifetime | A notion of when the object is created and destroyed, and thus when it is available for use |

source code the object may be referenced. The manner in which memory is allocated for the object determines its lifetime and places a second restriction on _when_ such references may occur during program execution.

# 11.2 SCOPE

Most programmers really do not take full advantage of the capability to limit accessibility provided by scope. Declarations are usually placed only in one of two locations: (1) outside of all functions to create global variables or (2) immediately following a function header to create temporary variables local to the function.

A more enlightened knowledge of scope, however, allows us to further restrict accessibility, providing better defense against accidental misuse of an object (Figure 11-1).

```
int a ;               /* global object (accessible by any function) */
void f( )
{
    int b ;           /* temporary local (accessible only inside f) */
    b = ... ;
    ...
}
```

FIGURE 11-1 Typical use of global and local scope.

# 11.2.1 Refining Local Scope

Simply stated, local scope refers to objects declared within a containing _block_. Blocks (which may be nested) begin with an opening curly brace and end with a matching closing curly brace. The scope of an object begins at its point of declaration and ends at the closing curly brace of its containing block. Objects declared within a block may not be referenced outside of that block. Thus:

+   1. The same identifier may be used for more than one object, as long as the objects are declared in different blocks; the correspondence between