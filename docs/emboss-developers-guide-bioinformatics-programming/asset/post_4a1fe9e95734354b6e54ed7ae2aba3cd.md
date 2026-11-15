
```c
AjPStr seqsubstring = NULL;
AjPDouble xarray = NULL;
```

Do not initialise declarations with functions. Never use for example:

```c
AjPStr seqsubstring = ajStrNew();
```

## C.6.5 Use of int, ajint, long and ajlong

To circumvent any problems arising from system-dependent sizes of variables (see Section 5.1, ‘Basic datatypes’), EMBOSS assumes an ajint is typically 32 bits and an ajlong is typically 64 bits (see Section 5.1, ‘Basic datatypes’). Use ajint, if 32 bits is enough, instead of int. Use ajlong instead of long or long long.

Match your datatype to what you need. If, for example, you are using an Alpha box then both your int and long variables will be 64 bits. In this case don’t use only ajlong out of laziness as your code will run more slowly on other platforms.

Standard C int and long should be used in some circumstances, for example, as parameters to C system library functions.

## C.7 Precedence of operators

Avoid confusion introduced by relying on operator precedence. This could be confusing:

```c
a = b * c + 1;
```

Whereas this is clear:

```c
a = (b * c) + 1;
```

## C.8 Structures and unions

### C.8.1 Declaration

All application datatypes and private datatypes defined in library source files should be declared static. Public datatypes declared in library header files should not include this keyword!

Always use the EMBOSS method of declaring structures and unions, i.e. using #define and typedef in the manner shown:

```c
typedef struct AjSStr
{
    ajuint Res;
    ajuint Len;
    char *Ptr;
    ajuint Use;
    ajint Padding;
} AjOStr;
#define AjPStr AjOStr*
typedef AjPStr* AjPPStr;
```

The declaration must contain a structure name (AjSStr), object name (AjOStr) and pointer name (AjPStr) even if these are not used. In the example above, a pointer to the object pointer is also defined (AjPPStr). This is optional and should only be included if needed.

### C.8.2 Naming conventions

The naming convention for AJAX public (external) structures is:

| Structure name | AjSName |
| Object name | AjOName |
| Pointer name | AjPName |

The naming convention for NUCLEUS public (external) structures is:

| Structure name | EmbSName |
| Object name | EmbOName |
| Pointer name | EmbPName |

Use of this convention, i.e. the P prefix for pointers, avoids problems where a pointer could appear to be an object in its own right.

This, for example, is bad practice in naming:

```c
typedef struct T *T;
...
T t;
```

It is not clear from the variable name that t is a pointer.

The naming convention for private structures drops the Aj and Emb prefix. For private structures whether in AJAX, NUCLEUS or application code use:

| Structure name | SName |
| Object name | OName |
| Pointer name | PName |

For example:

```c
/* @datastatic PBlastType *****************************************************
**
** DbiBlast types
**
** @attr ExtT [const char*] Table filename extension
** @attr ExtH [const char*] Header filename extension
** @attr ExtS [const char*] Sequence filename extension
** @attr IsProtein [AjBool] true for protein
** @attr IsBlast2 [AjBool] blast2.x or blast 1.x
** @attr Type [ajint] enumerated type
** @attr Padding [char[4]] Padding to alignment boundary
********************************************************************************/;

typedef struct SBlastType
{
    const char* ExtT;
    const char* ExtH;
    const char* ExtS;
    AjBool    IsProtein;
    AjBool    IsBlast2;
    ajint     Type;
    char      Padding[4];
} OBlastType;

#define PBlastType OBlastType*
```

### C.8.3 Datatype documentation

All public objects must be documented in a standard way (Appendix D, *Code documentation standards*). Separate individual objects by suitable whitespace (four newlines).

## C.9 Functions

### C.9.1 Function prototypes

All application functions and private functions in the libraries should be declared `static`. Public functions in the library should not include this keyword.

All functions must be prototyped using the full ANSI C style and indented for clarity. For example:

```c
/**
** Prototype definitions
*/

void             ajListPushAppend (AjPList list, AjPListNode* tail);
AjPList          ajListNewListref (const AjPList list);
void             ajListExit       (void);
AjBool           ajListPeekFirst  (const AjPList thys, void** x);
void             ajListFree       (AjPList *list);
```

### C.9.2 Implicit declarations

Examples of these would be:

```c
extern fubar(int x);
main(int argc, char **argv)
```

Do not use them. Always specify what a function should return. This is better:

```c
extern int fubar(int x);
int main(int argc, char **argv)
```

### C.9.3 Function and parameter names

Application function names should be:

- Prepended with the application name (lower-case) followed by an underscore: applicationname_FunctionName
- Meaningful
- As short as possible
- Given in ‘Sentence case’ where the name has more than one word
- Use alphabetic characters only (other than the single underscore).

for example:

```c
static void abiview_TextDisplay(AjPGraph graphs, ajint nstart, ajint nstop,
                                const AjPStr nseq, float tmax, float scale);
static ajint abiview_getResColour(char B);
```

Library function and function parameter names follow all but the first of the above conventions, additionally:

- All AJAX public (external) functions should begin with aj
- All NUCLEUS public (external) functions should begin with emb.

for example:

```c
AjBool ajStrAssignSubs(AjPStr* Pstr, const AjPStr str,
                         ajint pos1, ajint pos2);
double embIepPhFromHconc (double H);
```

When functions are added to the existing AJAX and NUCLEUS library files, and the changes are to be incorporated into the distribution, the function and parameter names must adhere to rules (Appendix D, *Code documentation standards*) that are defined in the header file and marked up in the code with the tag @namXrule.

### C.9.4 Function layout

The recommended order for the layout of code in functions is as follows:

- Variable declarations
- Calls to constructor functions
- Body of function
- Calls to destructor functions and return.

Always explicitly state a return at the end of every function, even for void functions.

For example:

```c
/* @func ajStrAssignK *****************************************************
**
** Copy a single character to a string.
**
** @param [w] Pstr [AjPStr*] Target string.
** @param [r] chr [char] Source text.
**
** @return [AjBool] ajTrue if string was reallocated
**
** @@@
****************************************************************************/

AjBool ajStrAssignK(AjPStr* Pstr, char chr)
{
    AjBool ret = ajFalse;
    AjPStr thys;

    if(!*Pstr)
        *Pstr=ajStrNewRes(2);

    thys = *Pstr;

    if(thys->Use != 1 || thys->Res <= 1)
    {
        ret = ajStrSetRes(Pstr, 2);
        thys = *Pstr;
    }

    thys->Ptr[0] = chr;
    thys->Ptr[1] = '\0';
    thys->Len =1;

    return ret;
}
```

### C.9.5 Function documentation

All public (external) functions must be documented in a standard way (Appendix D, *Code documentation standards*). Separate objects by suitable whitespace (four newlines).

## C.10 Program flow

### C.10.1 Loops

Do not use `continue` statements without good reason in large blocks of code as they can make it difficult to follow.

### C.10.2 goto

Do not use `goto`, or indeed functions for non-local jumps, unless there is really no alternative. They make code very difficult to follow.

### C.10.3 switch statements

Consider using `switch` statements to improve the readability of code where you have excessively long chains of `if else` statements. Where the same `switch` statement is duplicated throughout the code, however, this will be difficult to maintain. Consider changing your code (probably the data model) so that the `switch` is not needed.

## C.11 Memory allocation

### C.11.1 General memory management

Do not define large arrays in variable declarations within functions. They will go on the stack and can cause many problems.

Do not explicitly use `malloc()` or `calloc()`; instead use the AJAX macros, e.g. `AJALLOC`, `AJNEW`, `AJCNEW`, `AJNEW0`, `AJCNEW0`, etc. (see Section 5.3, ‘Objects (C data structures)’).

### C.11.2 Object construction

Call constructor functions explicitly, i.e. like this:

```c
int main(int argc, char **argv)
{
    AjPStr tmpstr = NULL;

    tmpstr = ajStrNew();
    ajStrAssignC(&tmpstr, "Hello");
}
```

not like this where construction occurs (the default string constructor is invoked by `ajStrAssignC`) but is not clear from the code:
