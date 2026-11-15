# 5.5 PROGRAMMING WITH OBJECTS

```
**
** @param [r] str [const AjPStr] String
** @param [r] str2 [const AjPStr] Second String
** @return [AjBool] ajTrue if two complete strings are the same
** @@
**********************************************************************************/
AjBool ajStrMatchS(const AjPStr str, const AjPStr str2)
{
    if(!str || !str2)
        return ajFalse;

    if(!strcmp(str->Ptr, str2->Ptr))
        return ajTrue;

    return ajFalse;
}
```

It is passed two AJAX string objects and uses the C function strcmp to compare the C-type strings in the object, returning ajTrue if they are the same or ajFalse otherwise. The function merely reads the value of the strings passed so will never need to allocate memory.

ajStrAssignS is different. This function assigns the value of one string to another. The string is copied rather than just setting a reference (pointer) to the original:

```
/* @func ajStrAssignS **********************************************************
**
** Copy a string to a string.
**
** This is a genuine copy (reference count isn't used). Useful where both
** strings will be separately overwritten later so that they can both remain
** modifiable.
**
** @param [w] Pstr [AjPStr*] Target string.
** @param [rN] str [const AjPStr] Source string.
** @return [AjBool] ajTrue if string was reallocated
** @@
******************************************************************************/
AjBool ajStrAssignS(AjPStr* Pstr, const AjPStr str)
{
    AjBool ret = ajFalse;
    AjPStr thys;

    if(!str)
    {
        return ajStrAssignC(Pstr, "");
    }

    ret = ajStrSetRes(Pstr, str->Len+1); /* minimum reserved size, OR more */
    thys = *Pstr;

    thys->Len = str->Len;
    memmove(thys->Ptr, str->Ptr, str->Len+1);

    return ret;
}
```