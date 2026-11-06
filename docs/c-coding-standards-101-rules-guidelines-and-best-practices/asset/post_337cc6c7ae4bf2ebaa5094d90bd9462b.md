
## 15. Use const proactively.

### Summary

**const** is your friend: Immutable values are easier to understand, track, and reason about, so prefer constants over variables wherever it is sensible and make **const** your default choice when you define a value: It’s safe, it’s checked at compile time (see Item 14), and it’s integrated with C++’s type system. Don’t cast away **const** except to call a const-incorrect function (see Item 94).

### Discussion

Constants simplify code because you only have to look at where the constant is defined to know its value everywhere. Consider this code:

```cpp
void Fun( vector<int>& v) {
    // ...

    const size_t len = v.size();

    // ... 30 more lines ...
}
```

When seeing **len**’s definition above, you gain instant confidence about **len**’s semantics throughout its scope (assuming the code doesn’t cast away **const**, which it should not do; see below): It’s a snapshot of **v**’s length at a specific point. Just by looking up one line of code, you know **len**’s semantics over its whole scope. Without the **const**, **len** might be later modified, either directly or through an alias. Best of all, the compiler will help you ensure that this truth remains true.

Note that **const** is not deep. For example, consider a class C that has a member of type X*. In C’s objects that are **const**, the X* member is also **const**—but the X object that is pointed to is not. (See [Saks99].)

Implement logical constness with **mutable** members. When a **const** member function of a class legitimately needs to modify a member variable (i.e., when the variable does not affect the object’s observable state, such as cached data), declare that member variable **mutable**. Note that all private members are hidden using the Pimpl idiom (see Item 43), **mutable** is not needed on either the cached information or the unchanging pointer to it.

Yes, const is “viral”—add it in one place, and it wants to propagate throughout your code as you call other functions whose signatures aren’t yet const-correct. This is a feature, not a bug, and this quality greatly increases **const**’s power even though it was unjustly demeaned in the days when **const** wasn’t well understood and appreciated. Retrofitting an existing code base to make it const-correct takes effort, but it is worthwhile and likely to uncover latent bugs.

Const-correctness is worthwhile, proven, effective, and highly recommended. Understanding how and where a program’s state changes is vital, and **const** documents that directly in code where the compiler can help to enforce it. Writing **const** appropriately helps you gain a better understanding of your design and makes your code sturdier and safer. If you find it impossible to make a member function **const**, you usually gain a better understanding of the ways in which that member function might modify an object’s state. You might also understand which data members bridge the gap between physical constness and logical constness, as noted in the following Examples.

Never cast away **const** except to call a const-incorrect function, or in rare cases as a workaround for lack of **mutable** on older compilers.

### Examples

*Example: Avoid **const** pass-by-value function parameters in function declarations.* The following two declarations are exactly equivalent:

```cpp
void Fun( int x );

void Fun( const int x );    // redeclares the same function; top-level const is ignored
```

In the second declaration, the **const** is redundant. We recommend declaring functions without such top-level **consts**, so that readers of your header files won’t get confused. However, the top-level **const** does make a difference in a function’s *definition* and can be sensible there to catch unintended changes to the parameter:

```cpp
void Fun( const int x ) {      // Fun’s actual definition
// ...

    ++x;                        // error: cannot modify a const value

// ...
}
```

### References

*[Allison98] §10 • [Cline99] §14.02-12 • [Dewhurst03] §6, §31-32, §82 • [Keffer95] pp. 5-6 • [Koenig97] §4 • [Lakos96] §9.1.6, §9.1.12 • [Meyers97] §21 • [Murray93] §2.7 • [Stroustrup00] §7.2, §10.2.6, §16.3.1 • [Sutter00] §43*

---

## 16. Avoid macros.

### Summary

TO_PUT_IT_BLUNTLY: Macros are the bluntest instrument of C and C++’s abstraction facilities, ravenous wolves in functions’ clothing, hard to tame, marching to their own beat all over your scopes. Avoid them.

### Discussion

It’s hard to find language that’s colorful enough to describe macros, but we’ll try. To quote from [Sutter04] §31:

> Macros are obnoxious, smelly, sheet-hogging bedfellows for several reasons, most of which are related to the fact that they are a glorified text-substitution facility whose effects are applied during preprocessing, before any C++ syntax and semantic rules can even begin to apply.

Lest there remain any ambiguity on this point, we note also that Bjarne Stroustrup has written:

> I dislike most forms of preprocessors and macros. One of C++’s aims is to make C’s preprocessor redundant (§4.4, §18) because I consider its actions inherently error prone. —[Stroustrup94] §3.3.1

> Macros are almost never necessary in C++. Use **const** (§5.4) or **enum** (§4.8) to define manifest constants [see Item 15], **inline** (§7.1.1) to avoid function-calling overhead [but see Item 8], **templates** (Chapter 13) to specify families of functions and types [see Items 64 through 67], and **namespaces** (§8.2) to avoid name clashes [see Items 57 through 59]. —[Stroustrup00] §1.6.1

> The first rule about macros is: Don’t use them unless you have to. Almost every macro demonstrates a flaw in the programming language, in the program, or in the programmer. —[Stroustrup00] §7.8

The main problem with C++ macros is that they seem much better at what they do than they really are. Macros ignore scopes, ignore the type system, ignore all other language features and rules, and hijack the symbols they **#define** for the remainder of a file. Macro invocations look like symbols or function calls, but are neither. Macros are not “hygienic,” meaning that they can expand to significantly and surprisingly different things depending on the context in which they are used. The text substitution that macros perform makes writing even remotely proper macros a black art whose mastery is as unrewarding as it is tedious.

People who think that template-related errors are the worst to decipher probably haven't seen those caused by badly formed or badly used macros. Templates are part of C++'s type system and thus allow compilers to get better at handling them (which they do), whereas macros are forever divorced from the language and hence intractable. Worse, unlike a template, a macro might expand to some transmission line noise that undesirably compiles by pure chance. Finally, an error in a macro can only be reported after the macro is expanded and not when it is defined.

Even in the rare cases where you do legitimately write a macro (see Exceptions), never ever even consider starting to think about writing a macro that is a common word or abbreviation. Do #undef macros as soon as possible, always give them SCREAMING_UPPERCASE_AND_UGLY names, and avoid putting them in headers.

### Examples

Example: Passing a template instantiation to a macro. Macros barely understand C++'s parentheses and square brackets well enough to balance them. C++, however, defines a new parenthetical construct, namely the < and > used in templates. Macros can't pair those correctly, which means that in a macro invocation

```cpp
MACRO( Foo<int, double> )
```

the macro thinks it is being passed two arguments, namely `Foo<int` and `double>`, when in fact the construct is one C++ entity.

### Exceptions

Macros remain the only solution for a few important tasks, such as #include guards (see Item 24), #ifdef and #if defined for conditional compilation, and implementing assert (see Item 68).

For conditional compilation (e.g., system-dependent parts), avoid littering your code with #ifdefs. Instead, prefer to organize code such that the use of macros drives alternative implementations of one common interface, and then use the interface throughout.

You may want to use macros (cautiously) when the alternative is extreme copying and pasting snippets of code around.

We note that both [C99] and [Boost] include moderate and radical extensions, respectively, to the preprocessor.

### References

[Boost] • [C99] • [Dewhurst03] §25-28 • [Meyers96] §1 • [Lakos96] §2.3.4 • [Stroustrup94] §3.3.1 • [Stroustrup00] §1.6.1, §7.8 • [Sutter00] §34-35 • [Sutter04] §31 • [Sutter04a]
