People who think that template-related errors are the worst to decipher probably haven't seen those caused by badly formed or badly used macros. Macros are templates are part of C++'s type system and thus allow compilers to get better at handling them (which they do), whereas macros are forever divorced from the language and hence intractable. Worse, unlike a template, a macro might expand to some transmission line noise that undesirably compiles by pure chance. Finally, an error in a macro can only be reported after the macro is expanded and not when it is defined.

Even in the rare cases where you do legitimately write a macro (see Exceptions), never ever even consider starting to think about writing a macro that is a common word or abbreviation. Do #undefine macros as soon as possible, always give them SCREAMING_UPPERCASE_AND_UGLY names, and avoid putting them in headers.

# ### Examples

Example: Passing a template instantiation to a macro. Macros barely understand C's parentheses and square brackets well enough to balance them. C++, however, defines a new parenthetical construct, namely the < and > used in templates. Macros can't pair those correctly, which means that in a macro invocation

```
```
MACRO( Foo<int, double> )
```
```

the macro thinks it is being passed two arguments, namely Foo<int and double>, when in fact the construct is one C++ entity.

# ### Exceptions

Macros remain the only solution for a few important tasks, such as #include guards (see Item 24), #ifdef and #if defined for conditional compilation, and implementing assert (see Item 68).

For conditional compilation (e.g., system-dependent parts), avoid littering your code with #ifdefs. Instead, prefer to organize code such that the use of macros drives alternative implementations of one common interface, and then use the interface throughout.

You may want to use macros (cautiously) when the alternative is extreme copying and pasting snippets of code around.

We note that both [C99] and [Boost] include moderate and radical extensions, respectively, to the preprocessor.

# ### References

[Boost] • [C99] • [Dewhurst03] §25-28 • [Meyers96] §1 • [Lakos96] §2.3.4 • [Stroustrup94] §3.3.1 • [Stroustrup00] §1.6.1, §7.8 • [Sutter00] §34-35 • [Sutter04] §31 • [Sutter04a]