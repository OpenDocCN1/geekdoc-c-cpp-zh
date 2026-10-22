
## Initializing External Variables

Like automatic variables, external variables can be initialized explicitly. Unlike automatic variables, external variables are initialized automatically to zero if you don’t initialize them. This rule applies to elements of an externally defined array, too. Unlike the case for automatic variables, you can use only constant expressions to initialize file scope variables:

```
int x = 10;          // ok, 10 is constant
int y = 3 + 20;      // ok, a constant expression
size_t z = sizeof(int); // ok, a constant expression
int x2 = 2 * x;      // not ok, x is a variable
```

(As long as the type is not a variable array, a sizeof expression is considered a constant expression.)

## Using an External Variable

Let’s look at a simple example that involves an external variable. Specifically, suppose you want two functions, call them main() and critic(), to have access to the variable units. You can do this by declaring units outside of and above the two functions, as shown in Listing 12.4. (Note: The intent of this example is to show how an external variable works, not to show a typical use.)

### Listing 12.4 The global.c Program

```
/* global.c -- uses an external variable */
#include <stdio.h>
int units = 0;        /* an external variable      */
void critic(void);
int main(void)
{
    extern int units;  /* an optional redeclaration */

    printf("How many pounds to a firkin of butter?\n");
    scanf("%d", &units);
    while ( units != 56 )
        critic();
    printf("You must have looked it up!\n");

    return 0;
}

void critic(void)
{
    /* optional redeclaration omitted */
    printf("No luck, my friend. Try again.\n");
    scanf("%d", &units);
}
```

Here is some sample output:

```
How many pounds to a firkin of butter?
14
No luck, my friend. Try again.
56
You must have looked it up!
```

(We did.)

Note how the second value for units was read by the critic() function, yet main() also knew the new value when it finished the while loop. So both the main() function and the critic() function use the identifier units to access the same variable. In C terminology, we say that units has file scope, external linkage, and static storage duration.

We made units an external variable by defining it outside of (that is, external to) any function definition. That's all you need to do to make units available to all the subsequent functions in the file.

Let's look at some of the details. First, declaring units where it is declared makes it available to the functions below it without any further action taken. Therefore, critics() uses the units variable.

Similarly, nothing needed to be done to give main() access to units. However, main() does have the following declaration in it:

```
extern int units;
```

In the example, this declaration is mainly a matter of documentation. The storage class specifier extern tells the compiler that any mention of units in this particular function refers to a variable defined outside the function, perhaps even outside the file. Again, both main() and critic() use the externally defined units.

## External Names

The C99 and C11 standards require compilers to recognize the first 63 characters for local identifiers and the first 31 characters for external identifiers. This revises the previous requirement of recognizing the first 31 characters for local identifiers and the first six characters for external identifiers. It's possible that you may be working with the old rules. The reason the rules for names of external variables are more restrictive than for local variables is that external names need to comply with the rules of the local environment, which may be more limiting.

## Definitions and Declarations

Let's take a longer look at the difference between defining a variable and declaring it. Consider the following example:

```
int tern = 1;        /* tern defined */
main()
{
    external int tern; /* use a tern defined elsewhere */
```

Here, tern is declared twice. The first declaration causes storage to be set aside for the variable. It constitutes a definition of the variable. The second declaration merely tells the compiler to use the tern variable that has been created previously, so it is not a definition. The first declaration is called a defining declaration, and the second is called a referencing declaration. The keyword extern indicates that a declaration is not a definition because it instructs the compiler to look elsewhere.

Suppose you do this:

```
extern int tern;
int main(void)
{
```

The compiler will assume that the actual definition of tern is somewhere else in your program, perhaps in another file. This declaration does not cause space to be allocated. Therefore, don’t use the keyword extern to create an external definition; use it only to refer to an existing external definition.

An external variable can be initialized only once, and that must occur when the variable is defined. Suppose you have this:

```
// file one.c
char permis = 'N';
...
// file two.c
extern char permis = 'Y';  /* error */
```

This is an error because the defining declaration in file_one.c already has created and initialized permis.

## Static Variables with Internal Linkage

Variables of this storage class have static storage duration, file scope, and internal linkage. You create one by defining it outside of any function (just as with an external variable) with the storage class specifier static:

```
static int svil = 1;  // static variable, internal linkage
int main(void)
{
```

Such variables were once termed external static variables, but that’s a bit confusing because they have internal linkage. Unfortunately, no new compact term has taken the place of external static, so we’re left with static variable with internal linkage. The ordinary external variable can be used by functions in any file that’s part of the program, but the static variable with internal linkage can be used only by functions in the same file. You can redeclare any file scope variable within a function by using the storage class specifier extern. Such a declaration doesn’t change the linkage. Consider the following code:

```
int traveler = 1;      // external linkage
static int stayhome = 1; // internal linkage
int main()
{
    extern int traveler;  // use global traveler
    extern int stayhome;  // use global stayhome
    ...
```

Both traveler and stayhome are global for this particular translation unit, but only traveler can be used by code in other translation units. The two declarations using extern document that main() is using the two global variables, but stayhome continues to have internal linkage.

## Multiple Files

The difference between internal linkage and external linkage is important only when you have a program built from multiple translation units, so let’s take a quick look at that topic.

Complex C programs often use several separate files of source code. Sometimes these files might need to share an external variable. The C way to do this is to have a defining declaration in one file and referencing declarations in the other files. That is, all but one declaration (the defining declaration) should use the extern keyword, and only the defining declaration should be used to initialize the variable.

Note that an external variable defined in one file is not available to a second file unless it is also declared (by using extern) in the second file. An external declaration by itself only makes a variable potentially available to other files.

Historically, however, many compilers have followed different rules in this regard. Many Unix systems, for example, enable you to declare a variable in several files without using the extern keyword, provided that no more than one declaration includes an initialization. If there is a declaration with an initialization, it is taken to be the definition.

## Storage-Class Specifier Roundup

You may have noticed that the meaning of the keywords static and extern depends on the context. The C language has six keywords that are grouped together as storage-class specifiers. They are auto, register, static, extern, _Thread_local, and typedef. The typedef keyword doesn’t say anything about memory storage, but it is thrown in for syntax reasons. In particular, in most cases you can use no more than one storage-class specifier in a declaration, so that means you can’t use one of the other storage-class specifiers as part of a typedef. The one exception is that _Thread_local may be used together with static and extern.

The auto specifier indicates a variable with automatic storage duration. It can be used only in declarations of variables with block scope, which already have automatic storage duration, so its main use is documenting intent.
