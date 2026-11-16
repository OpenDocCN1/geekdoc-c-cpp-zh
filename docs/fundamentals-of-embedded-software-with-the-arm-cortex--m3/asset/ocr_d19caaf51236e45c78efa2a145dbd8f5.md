```
/* defining file; do initializations here ... */
int a = 123; /* externally visible */
static int b = 0; /* local to file */
void f1() {
...
}

/* referencing file; no initializations here ... */
void f2() {
extern int a;
a = ... /* actual reference */
}
```

# FIGURE 11-2 Accessing data across multiple source files.

Within the referencing file, the identifier's scope is determined by the position of
the extern declaration. If the declaration is global, then the identifier is global to the
file; placing the declaration within a block makes it local to that block.

Although the keyword extern is required to establish an interfile reference to a
global object, it leaves control in the hands of the reference rather than the definition. It
offers no protection against interfile references that the programmer had not intended.
Adding the keyword static to the declaration of a global object restricts its scope
to the file in which it is declared.1 This nonintuitive feature of the static keyword causes
the object's identifier to be hidden from the link process, and it eliminates any possibil-
ity of a syntactic reference from within other files.

Since this feature of the static keyword is not particularly intuitive, many pro-
grammers create a macro to make their intention clear, as in the following code:
#define LOCAL2FILE static
...
LOCAL2FILE int b = 0; /* This 'b' is not accessible from other files! */

Functions are inherently global. Although a function-prototype declaration is
usually necessary in the referencing file to specify the number and type of parameters,
the prototype does not need to include the keyword extern to establish an interfile
reference. The linker automatically resolves interfile function references unless the
function definition begins with the keyword static.

# 11.3 LIFETIME

Objects are created, initialized, used, and destroyed. The notion of lifetime refers to the
duration of an object's existence (i.e., when it is accessible), determines how objects are