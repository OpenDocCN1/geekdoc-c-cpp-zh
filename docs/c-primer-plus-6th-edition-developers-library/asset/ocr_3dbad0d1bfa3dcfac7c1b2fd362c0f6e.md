# Setting Up the Structure Declaration

A *structure declaration* is the master plan that describes how a structure is put together. The declaration looks like this:

```
struct book {
    char title[MAXTITL];
    char author[MAXAUTL];
    float value;
};
```

This declaration describes a structure made up of two character arrays and one *float* variable. It does not create an actual data object, but it describes what constitutes such an object. (Occasionally, we’ll refer to a structure declaration as a *template* because it outlines how data will be stored. If you’ve heard of templates in C++, that’s a different, more ambitious use of the word.) Let’s look at the details. First comes the keyword *struct*. It identifies what comes next as a structure. Next comes an optional *tag*—the word *book*—that is a shorthand label you can use to refer to this structure. Therefore, later we have this declaration:

```
struct book library;
```

It declares *library* to be a structure variable using the *book* structure design.

Next in the structure declaration, the list of structure members are enclosed in a pair of braces. Each member is described by its own declaration, complete with a terminating semicolon. For example, the *title* portion is a *char* array with *MAXTITL* elements. A member can be any C data type—and that includes other structures!

A semicolon after the closing brace ends the definition of the structure design. You can place this declaration outside any function (externally), as we have done, or inside a function definition. If the declaration is placed inside a function, its tag can be used only inside that function. If the declaration is external, it is available to all the functions following the declaration in the file. For example, in a second function, you could define

```
struct book dickens;
```

and that function would have a variable, *dickens*, that follows the form of the *book* design.

The tag name is optional, but you must use one when you set up structures as we did, with the structure design defined one place and the actual variables defined elsewhere. We will return to this point soon, after we look at defining structure variables.

# Defining a Structure Variable

The word *structure* is used in two senses. One is the sense “structure plan,” which is what we just discussed. The structure plan tells the compiler *how* to represent the data, but it doesn’t make the computer *allocate* space for the data. The next step is to create a *structure variable*, the