# A.6 Template Details

```
void g()
{
    c1::c2::cc o;
    const c1::c2::cc c(o);
    f(o);
    f(c);
} // void f(c1::c2::cc& o) } // #3
} // namespace f2
} // namespace f1
```

For the const object c, only overload #2 is admissible and that one is visible. Fine, case closed. For the mutable object o, we need a closer look. The last overload of f (f #3) is defined after g and therefore not visible in g. The global function f is hidden by #2. Thus remain #1 and #2 of which the former is the better match (no implicit conversion to const).

Summarizing, the general strategy for determining which function overload is called consists of three steps:

+   1. Find all overloads defined before the call
+      * In the namespace of the caller;
+      * In its parent namespaces;
+      * In the namespace of the arguments (ADL);
+      * In imported namespaces (using directive); and
+      * By imported names (using declaration).
+   If this set is empty, the program will not compile.
+   2. Eliminate the hidden overloads.
+   3. Select the best match among the available overloads. If this is ambiguous, the program will not compile.

The examples in this sub-section were certainly somewhat tiresome, but as Monk would say: “You will thank me later.” The good news is: in your future programmer’s life it will rarely be as bad as our made-up examples.

# A.6.3 Specializing for Specific Hardware

Speaking of platform-specific assembler hacks, maybe we are eager to contribute code that explores SSE units by performing two computations in parallel. This might look like the following:

```
template <typename Base, typename Exponent>
Base inline power(const Base& x, const Exponent) { ... }

#ifdef SSE_FOR_TRYPTICHON_WQ_OMICRON_LXXXVI_SUPPORTED
std::pair<double> inline power(std::pair<double> x, double y)
{
    asm ("
    # Yo, I'm the greatest geek under the sun!
```