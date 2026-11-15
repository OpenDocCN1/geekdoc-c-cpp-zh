
### C.2.3.3 Braces

Matching braces should appear in the same column and indentation should be consistent. This is good:

```c
int fred(void)
{
    ...
    for(i=0; i<LIMIT; ++i)
    {
        ...
    }
    return 0;
}
```

whereas this is messy:

```c
int fred(void) {
    ...
    for(i=0; i<LIMIT; ++i) {
        ...
    }
    return 0;
}
```

and so is this:

```c
int fred(void)
{
    ...
    for(i=0; i<LIMIT; ++i)
        {
        ...
        } ...
    return 0;
}
```

Don't use braces unnecessarily. The following is good:

```c
for(i=0; i<LIMIT; ++i)
    sum += i;
```

but this code is cluttered:

```c
for(i=0; i<LIMIT; ++i)
{
    sum += i;
}
```

The body of a for statement should appear in its own block distinct from the for statement itself. The following could be confusing if nested in a larger body of code:

```
for (i=0; i<LIMIT; ++i) sum += i;
```

### C.2.3.4 Indentation

Indentation of four characters is recommended but, more importantly, be consistent. If you find that indentation within nested loops results in many of the lines wrapping then you should check whether the code structure can be improved.

There are some lines you can add to your .emacs file which will (usually) automatically place braces in the correct places and indent properly. They are available in the file http://emboss.open-bio.org/downloads/EmacsConfig and are shown below:

```
(defun set-if-void (symbol value)
 (or (boundp symbol)
   (set symbol value)))

(require 'cc-mode)
(setq auto-mode-alist
   (append
     '(("\\.C$" . c++-mode)
       ("\\.H$" . c++-mode)
       ("\\.cc$" . c++-mode)
       ("\\.hh$" . c++-mode)
       ("\\.c$" . c-mode)
       ("\\.h$" . c-mode)
       ("\\.m$" . objc-mode)
       ("\\.java$" . java-mode))
     auto-mode-alist))

(defconst emboss-c-style
   '((c-tab-always-indent
     . t)
   (c-comment-only-line-offset
     . 0)
   (c-hanging-braces-alist
     . ((brace-list-open)))
   (c-hanging-colons-alist
     . ((member-init-intro before)
       (inher-intro)
       (case-label after)
       (label after)
       (label after)))
   (c-cleanup-list
   . (scope-operator
      empty-defun-braces
      defun-close-semi))

;; Uncomment the following line if you don't want newlines after semicolons
;;   (c-hanging-semi&comma-criteria)
   (c-offsets-alist
     . ((arglist-close . c-lineup-arglist)
        (substatement-open . 0)
        (case-label . 4)
        (block-open . 0)
        (knr-argdecl-intro . -))))

)
"EMBOSS C Programming Style")

;; Customisations for all of c-mode, c++-mode, and objc-mode
(defun emboss-c-mode-common-hook ()
 ;; add EMBOSS style and set it for the current buffer
(c-add-style "EMBOSS" emboss-c-style t)
;; offset customisations not in emboss-c-style
(c-set-offset 'member-init-intro '++)
;; other customisations
(setq tab-width 8
      ;; this will make sure spaces are used instead of tabs
      indent-tabs-mode nil)
;; auto-newline [for hungry-delete use (c-toggle-auto-hungry-state 1)]
(c-toggle-auto-state 1)

;; keybindings for C, C++, and Objective-C. Can put these in
;; c-mode-map because c++-mode-map and objc-mode-map inherit it
(define-key c-mode-map "\C-m" 'newline-and-indent)
)

(add-hook 'c-mode-common-hook 'emboss-c-mode-common-hook)
```

This will also let you reformat existing code (with some manual intervention) using the emacs command M-x indent-region.

## C.3 ANSI C standard

EMBOSS C source code should follow the ANSI C standard (ANSI X3.159-1989 ‘Programming Language C’). This version of the language is often referred to as ‘ANSI C’, ‘Standard C’ or ‘C89’. The semantics of this are given in the book:

> The C Programming Language, 2nd edn
> Brian Kernighan and Dennis Ritchie
> Prentice Hall 1988; ISBN 0-13-110362-8

For a definitive reference manual, see:

> C: A Reference Manual, 5th edn
> Samuel P. Harbison and Guy L. Steele
> Prentice Hall 2002; ISBN 0-13-089592-X.

This standard introduced:

- Function prototypes
- C++ style parameter declarations (argument types are specified in the function declarations)
- void pointers
- Support for international character sets and locales
- A more capable preprocessor
- Enumerated types (enum)
- Ability to pass structures to functions and have structures as return values.

Most of these are welcome additions. In EMBOSS, passing whole structures around is deprecated because it can be wasteful of stack memory and rather slow. Each EMBOSS object (C data structure) has a pointer defined for it which should be used for referencing (see below).

If you need to write system-dependent code then try to put such functions in a separate header file to isolate them as much as possible. The AJAX library file ajsys.c may well be suitable for such code. Remember that your code will need to work under many operating systems, e.g. Linux, Windows, MacOSX, etc.

## C.4 Use of the pre-processor

The contents of every header (*.h) file must be enclosed in the pre-processor directives shown above.

The pre-processor can be used for:

- System-dependent code (but see the ajsys corollary above.)
- Commenting out code with #if 0
- Conditionals arising from system limits
- Definitions (#define); but consider enum or static const instead (see below).

An example of a conditional arising from system limits:

```c
#include <limits.h>

#if INT_MAX > UCHAR_MAX
...
#else
#error "need int wider than char"
#endif
```

### C.4.1 Constants

For constants, consider using enum and variables instead of #define, which is rarely visible in debuggers. For example:

```c
enum { Red = 0xF00, Blue = 0x0F0, Green = 0x00F };
static const float pi = 3.14159265358;
```

### C.4.2 Macros

Macros should avoid side effects. If possible, mention each argument exactly once. Put parentheses around all arguments. When the macro is an expression, put parentheses around the whole macro body. If the macro is the inline expansion of some function then capitalise the name and precede it with M:

```c
#define MAJFUBAR (X) \
(save = (X), \
dosomethingwith(X);
(X) = save);
```

Try to write macros so that they are syntactically expressions, i.e. so you can put a semicolon at the end of their use.

## C.5 Comments

Avoid fancy layout or decoration in comments. The styles used are as follows:

```
/* single line comments look like this */

/*
** Important single line comments look like multi-line comments.
*/

/*
** Multi-line comments look like this. Put the opening and closing
** comment sequences on lines by themselves. Use complete sentences
** with proper English grammar, capitalisation and punctuation.
*/

/* but you don't need to punctuate or capitalise one-liners */
```

The opening forward slash (/) of all comments should be indented to the same level as the code to which it applies, for example:

```c
if (fubar())
{
    /* Print a message before exiting. */
    ajFatal("Program is FUBAR");
}
```

Avoid placing comments on the same line as the code itself. If, for tidiness, they are deemed essential, then set it off from the code using spaces. Try to indent such comments to the same column and don't continue them across multiple lines:

```c
func1(); /* useless comment */
func2(); /* useless comment */
func3(); /* useless comment */
```

See Section 3.1, 'EMBOSS programming' for guidelines on when and how to use comments.

## C.6 Variables

### C.6.1 Global variables

Do not use them without a very compelling reason because they tend to make code very difficult to understand. If used sparingly and judiciously in some circumstances however they can greatly simplify the code. Use your discretion.

### C.6.2 Static variables in functions

Such functions are not re-entrant so do not use them at all if you’d like the code to work in multi-threaded contexts. Occasionally there is very strong reason to use them but avoid them otherwise.

### C.6.3 Variable declarations

Declare all variables at the top of each function. Declare one variable per line. It is easier to read if both datatypes and variables line up. This is tidy:

```c
{
    ajint   a;
    ajint   b;
    ajlong  c;
    ...
}
```

whereas this is messy:

```c
{
    ajint a,b;
    ajlong c;
    ...
}
```

This following code would conform to the latest C standard (C99) but is unclear (and C99 isn’t supported by all the platforms on which EMBOSS should work):

```c
{
    .
    .
    .
        for (ajint a=0; a<b; a++)
    .
    .
    .
}
```

The recommended layout is:

```c
{
    ajint a;
    ajint b;
    ...
    for (a=0; a<b; a++)
    .
    .
}
```

### C.6.4 Variable initialisation

Always initialise object pointer variables to NULL. There are circumstances in EMBOSS where it can be risky not to (see Section 5.3, ‘Objects (C data structures)’). Initialise other datatypes as appropriate in the code. Align initialisation statements for ease of reading:
