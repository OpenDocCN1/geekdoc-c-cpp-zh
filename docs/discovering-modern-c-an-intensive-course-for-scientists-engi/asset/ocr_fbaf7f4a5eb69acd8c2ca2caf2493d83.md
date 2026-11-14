```
/* int x78zy99= yo6952fq;     // start old comment
int x78zy9a= yo6951fq;     */ // end old comment
int x78zy9b= yo6958fq;     /*     // end new comment (presumably)
int x78zy9c= yo6949fq;
for ( ... ) {
```

Here, the line for setting x78zy9b should have been disabled but the preceding */ terminated the comment prematurely.

Nested comments can be realized (correctly) with the preprocessor directive #if as we will illustrate in Section 1.9.2.4. Another possibility to deactivate multiple lines conveniently is by using the appropriate function of IDEs and language-aware editors.

# 1.9.2 Preprocessor Directives

In this section, we will present the commands (directives) that can be used in preprocessing. As they are mostly language-independent, we recommend limiting their usage to an absolute minimum, especially macros.

# 1.9.2.1 Macros

> > “Almost every macro demonstrates a flaw in the programming language, in the program, or the programmer.”
> > —Bjarne Stroustrup

This is an old technique of code reuse by expanding macro names to their text definition, potentially with arguments. The use of macros gives a lot of possibilities to empower your program but much more for ruining it. Macros are resistant against namespaces, scopes, or any other language feature because they are reckless text substitution without any notion of types. Unfortunately, some libraries define macros with common names like `major`. We uncompromisingly undefine such macros, e.g., `#undef major`, without mercy for people who might want use those macros. Visual Studio defines—even today!!!—`min` and `max` as macros, and we strongly advise you to disable this by compiling with `/DNOMINMAX`. Almost all macros can be replaced by other techniques (constants, templates, inline functions). But if you really do not find another way of implementing something:

# Macro Names

Use LONG_AND_UGLY_NAMES_IN_CAPITALS for macros!

Macros can create weird problems in almost every thinkable and unthinkable way. To give you a general idea, we look at few examples in Appendix A.2.10 with some tips for how to deal with them. Feel free to postpone the reading until you run into some issue.

As you will see throughout this book, C++ provides better alternatives like constants, inline functions, and `constexpr`.