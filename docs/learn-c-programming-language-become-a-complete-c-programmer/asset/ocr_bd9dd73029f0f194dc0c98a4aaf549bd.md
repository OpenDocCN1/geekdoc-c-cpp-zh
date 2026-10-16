are free of minor annoying technical restrictions.

+   - **Regular<X>**: X s are **Semiregular** and can be compared using equality. The standard-library containers require their elements to be regular.
+   - **Ordered<X>**: X s are **Regular** and **Totally_ordered.** The standard-library associative containers require their elements to be ordered unless you explicitly provide a comparison operation.
+   - **Assignable<X,Y>**: A **Y** can be assigned to an **X** using =.
+   - **Predicate<F,X>**: An **F** can be called for an **X** yielding a **bool**.
+   - **Streamable<X>**: An **X** can be read and written using iostreams.
+   - **Movable<X>**: An **X** can be moved; that is, it has a move constructor and a move assignment. In addition, an **X** is addressable and destructible.
+   - **Copyable<X>**: An **X** is **Movable** and can also be copied.
+   - **Convertible<X,Y>**: An **X** can be implicitly converted to a **Y**.
+   - **Common<X,Y>**: An **X** and a **Y** can unambiguously be converted to a common type called **Common_type<X,Y>**. This is a formalization of the language rule for compatibility of operands to ?: (§11.1.3). For example, **Common_type<Base_*,Derived_*>** is **Base_*** and **Common_type<int,long>** is **long**.
+   - **Range<X>**: An **X** that can be used by a rangefor (§9.5.1), that is, **X** must provide members, **x.begin()** and **x.end()**, or nonmember equivalents, **begin(x)** and **end(x)**, with the required semantics.

Obviously, these definitions are informal. In most cases, these concepts are based on standardlibrary type predicates (§35.4.1), and the ISO C++ standard provides formal definitions (e.g., §iso.17.6.3).

# 24.4.5 Template Definition Checking

A constraints-check template ensures that a type provides the properties required by the concept. If the implementation of a template in fact uses more properties than its concepts guarantee, we may get type errors. For example, the standard-library find() requires a pair of input iterators as arguments, but we might ( incautiously) have defined it like this:

```
template<typename Iter, typename Val>
Iter find(Iter b, Iter e, Val x)
{
static_assert(Input_iterator<Iter>(),"find(): Iter is not a Forward iterator");
static_assert(Equality_comparable<Value_type<Iter>,Val>, "find(): value type doesn’t match iterator");

while (b!=e) {
if (*b==x) return b;
b = b+1; // note: not ++b
}
return b;
}
```

Now, b+1 is an error unless b is a random-access iterator (and not just a forward iterator