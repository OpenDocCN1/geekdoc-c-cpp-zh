For example:

```
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

# C.8.3 Datatype documentation

All public objects must be documented in a standard way (Appendix D, *Code documentation standards*). Separate individual objects by suitable whitespace (four newlines).

# C.9 Functions

# C.9.1 Function prototypes

All application functions and private functions in the libraries should be declared `static`. Public functions in the library should not include this keyword.

All functions must be prototyped using the full ANSI C style and indented for clarity. For example:

```
/**
** Prototype definitions
*/

void             ajListPushAppend (AjPList list, AjPListNode* tail);
AjPList          ajListNewListref (const AjPList list);
void             ajListExit       (void);
AjBool           ajListPeekFirst  (const AjPList thys, void** x);
void             ajListFree       (AjPList *list);
```