# # The #undef Directive

The #undef directive “undefines” a given #define. That is, suppose you have this definition:

#define LIMIT 400

Then the directive

#undef LIMIT

removes that definition. Now, if you like, you can redefine LIMIT so that it has a new value. Even if LIMIT is not defined in the first place, it is still valid to undefine it. If you want to use a particular name and you are unsure whether it has been used previously, you can undefine it to be on the safe side.

# # Being Defined—The C Preprocessor Perspective

The preprocessor follows the same rules as C about what constitutes an identifier. An identifier can consist only of uppercase letters, lowercase letters, digits, and underscore characters, and a digit cannot be the first character. When the preprocessor encounters an identifier in a preprocessor directive, it considers it to be either defined or undefined. Here, defined means defined by the preprocessor. If the identifier is a macro name created by a prior #define directive in the same file and it hasn't been turned off by an #undef directive, it's defined. If the identifier is not a macro but is, say, a file-scope C variable, it's not defined as far as the preprocessor is concerned.

```
```c
#define LIMIT 1000 // LIMIT is defined
#define GOOD // GOOD is defined
#define A(X) ((-(X))*(X)) // A is defined
int q; // q not a macro, hence not defined
#undef GOOD // GOOD not defined
```
```

Note that the scope of a #define macro extends from the point it is declared in a file until it is the subject of an #undef directive or until the end of the file, whichever comes first. Also note that the position of the #define in a file will depend on the position of an #include directive if the macro is brought in via a header file.

A few predefined macros such as __DATE__ and __FILE__ (discussed later this chapter), are always considered defined and cannot be undefined.

# # Conditional Compilation

You can use the other directives mentioned to set up conditional compilations. That is, you can use them to tell the compiler to accept or ignore blocks of information or code according to conditions at the time of compilation.