Summarizing, the general strategy for determining which function overload is called consists of three steps:

+   1. Find all overloads defined before the call
+   
+   * In the namespace of the caller;
+   * In its parent namespaces;
+   * In the namespace of the arguments (ADL);
+   * In imported namespaces (using directive); and
+   * By imported names (using declaration).

If this set is empty, the program will not compile.

+   2. Eliminate the hidden overloads.

+   3. Select the best match among the available overloads. If this is ambiguous, the program will not compile.

The examples in this sub-section were certainly somewhat tiresome, but as Monk would say: “You will thank me later.” The good news is: in your future programmer’s life it will rarely be as bad as our made-up examples.

# A.6.3 Specializing for Specific Hardware

Regarding platform-specific assembler hacks, maybe we are eager to contribute code that explores SSE units by performing two computations in parallel. This might look like:

Click here to view code image

```
template <typename Base, typename Exponent>
Base inline power(const Base& x, const Exponent) { ... }
# ifdef SSE_FOR_TRYPTICHON_WQ_OMICRON_LXXXVI_SUPPORTED
std::pair<double> inline power(std::pair<double> x, double y)
{
    asm ("
    Yo, I'm the greatest geek under the sun!
    movapd xmm6, x
    ...
    "
    return whatever;
}
```