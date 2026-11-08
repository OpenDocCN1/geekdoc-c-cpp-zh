```
std::forward_iterator_tag;
```

With that, `std::iterator_traits<>` assumes `InputIterator<T>`, and we can now overload template constrained for both iterator categories.

# ## E.4 CONCEPT TIPS

Although C++ concepts have been worked on for many years now, and experimental implementations have been available in some form for over a decade, broad experience with them is just starting to emerge. We hope that a future edition of this book will be able to provide much more practical guidance about how to design constrained template libraries. Meanwhile, however, we offer three observations.

# ### E.4.1 Testing Concepts

Concepts are Boolean predicates that are valid constant-expressions. Therefore, given a concept C and some types T1, T2, ..., that model the concept, we can statically assert that observation:

*Click here to view code image*

```
static_assert(C<T1, T2, ...>, "model failure");
```

When designing concepts, it is therefore recommended to also design some types that test them in this way. That includes types that push the boundaries of what the concept entails, answering questions such as the following:

+   - Do interfaces and/or algorithms need to copy and/or move objects of the types being modeled?
+   - What conversions are acceptable? Which ones are needed?
+   - Is the basic set of operations assumed by the template unique? For example, can a type's operative signs be `++` or `--`?

Here, too, the notion of archetypes (see Section 18.3 on page 653) can be useful.

# ### E.4.2 Concept Granularity

With concepts becoming part of the C++ language, it is natural to want to build "libraries of concepts," just as we build class libraries and template libraries as soon as those features were available. As with other libraries, it is also natural to want to favor our concepts in various ways. We briefly discussed the example of iterator categories, and it's not a great leap to envision that we could build "range categories" alongside these and perhaps "sequence concepts" on top of those, and so on.

On the other hand, we might be tempted to build all of those concepts on top of "elementary syntax" concepts. For example, we could imagine:

*Click here to view code image*

```
template<typename T>
concept Addable =
  requires (T a, T b) {
    a + b;
  };
```

That is not recommended, however, because it is a concept that has no other semantic connotation, and disparate types will satisfy it. For example, it is satisfied when `T` and `U` are both `std::string` or when one type is a pointer and the other an integral type, and of course with arithmetic types. Yet in those three cases, the notion of Addable means something fundamentally different (respectively, concatenation, iterator displacement, and variants of arithmetic addition). Introducing such a concept is therefore a recipe for libraries with fairly interesting and likely to trigger odd ambiguities.

Instead, it appears that concepts are best designed to model real semantic notions that are in the problem domain. Doing so is a disciplined fashion. Doing so is bound to improve the overall design of our libraries, as it will bring intrinsically and clearly to the interfaces presented to our clients.

# ### E.4.3 Binary Compatibility

Experienced C++ programmers are aware that when certain entities (functions and member functions in particular) are compiled down to low-level machine code, a name is associated with them that combines the declared name with the type and scope of the entity. This name, commonly referred to as the mangled name of the entity, is what is used by object code linkers to resolve references to the entity (e.g., from other object files). For example, the mangled name of a function defined as

*Click here to view code image*