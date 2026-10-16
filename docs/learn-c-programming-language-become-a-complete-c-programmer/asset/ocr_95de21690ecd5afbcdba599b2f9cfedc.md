read and very hard to debug. Nontrivial uses of templates can also impact compile times. If you have a hard time understanding what is going on in code requiring complicated patterns of instantiation, so might the compiler. Worse still, so may the programmer who gets to maintain your code.

+   Template metaprogramming attracts clever people:
+   - Partly, that’s because metaprogramming allows us to express things that simply can’t be done at the same level of type safety and run-time performance. When the improvements are significant and the code maintainable, these are good – sometimes even compelling – reasons.
+   - Partly, that’s because metaprogramming allows us to show off our cleverness. Obviously, that is to be avoided.

How would you know that you have gone too far with metaprogramming? One warning sign that I use is an urge to use macros (§12.6) to hide “details” that have become too ugly to deal with directly. Consider:

```
#define IF(c,x,y) typename std::conditional<(c),x,y>::type
```

Is this going to far? It allows us to write

```
IF(cond,Cube,Square) z;
```

rather than

```
typename std::conditional<(cond),Cube,Square>::type z;
```

I have biased the question by using the very short name IF and the long form std::conditional.

# Section 28.3.3 When to Use Metaprogramming 795

Similarly, a more complex condition would almost equalize the number of characters used. The fundamental difference is that I have to write typename and ::type to use the standard’s terminology. That exposes the template implementation technique. I would like to hide that, and the macro does. However, if many people need to collaborate and programs get large, a bit of verbosity is preferable to a divergence of notations.

Another serious argument against the IF macro is that its name is misleading: conditional is not a “drop-in replacement” for a conventional if. That ::type represents a significant difference: conditional selects between types; it does not directly alter control flow. Sometimes it is used to select a function and thus represent a branch in a computation; sometimes it is not. The IF macro hides an essential aspect of its function. Similar objections can be leveled at many other “sensible” macros: they are named for some programmer’s particular idea of their use, rather than reflecting fundamental functionality.

In this case, the problems of verbosity, of the implementation details leaking out, and of poor naming are easily handled by a type alias (Conditional, §28.2.1). In general, look hard for ways to clean up the syntax presented to users without inventing a private language. Prefer systematic techniques, such as specialization and the use of aliases, to macro hackery. Prefer constexpr functions to templates for compile-time computation, and hide template metaprogramming implementation details in constexpr functions whenever feasible (§28.2.2).

Alternatively, we can look at the fundamental complexity of what we are trying to do: [1] Does it require explicit tests?