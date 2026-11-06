# 67. Don’t write unintentionally nongeneric code.

# **Summary**

Commit to abstractions, not to details: Use the most generic and abstract means to implement a piece of functionality.

# **Discussion**

When writing code, use the most abstract means available that get the job done. Think in terms of what operations put the least “capabilities strain” on the interfaces they operate on. This habit makes your code more generic, and therefore more reusable and more resilient to changes in its surroundings.

On the contrary, code that gratuitously commits to details is rigid and fragile:

+   - **Use `!=` instead of `<` to compare iterators:** Using `!=` is more general and so applies to a larger class of objects; using `<` asks for ordering, and only random-access iterators can implement `operator<`. If you use `operator!=` your code will “port” easily to other kinds of iterators, such as forward and bidirectional iterators.
+   - **Prefer iteration to indexed access:** Most containers don’t support indexed access; for example, `list` can’t implement it efficiently. But all containers support iterators. Iteration is a better approach because it is more general, and it can still be used in conjunction with indexed access as needed.
+   - **Use `empty()` instead of `size() == 0`:** “Empty/non-empty” is a more primitive concept than “exact size.” For example, you might not know the size of a stream but can always talk about emptiness, and the same applies to input iterators. Some containers, such as `list`, naturally implement `empty` more efficiently than `size`.
+   - **Use the highest class in the hierarchy that offers the functionality you need:** When programming with dynamic polymorphic classes, don’t depend on details you don’t need and that tie you to specific derived classes.
+   - **Write const-correct code (see Item 15):** Taking `const&` parameters puts less strain on the caller because `const&` covers constant and non-constant objects alike.

# **Exceptions**

In some cases, indexing instead of iteration enables compilers to do better optimization. Before you’re tempted to make use of this, make sure you really need it and that your compiler really does it. (See Item 8.)

# **References**

[Koenig97] §12.7, §17-18 • [Meyers01] §4 • [Stroustrup00] §13, §17.1.1 • [Sutter04] §1, §5, §34