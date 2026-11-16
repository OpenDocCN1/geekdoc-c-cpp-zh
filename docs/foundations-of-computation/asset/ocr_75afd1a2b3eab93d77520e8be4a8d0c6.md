is a valid argument. Here is a formal proof that

\(\frac{n \text{ is even}}{\therefore n^2 \text{ is even}}\)

is in fact a valid argument for any value of \(n\):

Let \(n\) be an arbitrary integer.

+   1. \(n\) is even ... premise
+   2. if \(n\) is even, then \(n = 2k\) ... definition of even
+   3. \(n = 2k\) for some integer \(k\) ... from 1, 2 (modus ponens)
+   4. if \(n = 2k\) for some integer \(k\), then \(n^2 = 4k^2\) for that integer \(k\) ... basic algebra
+   5. \(n^2 = 4k^2\) for some integer \(k\) ... from 3, 4 (modus ponens)
+   6. if \(n^2 = 4k^2\) for some integer \(k\), then \(n^2 = 2(2k^2)\) for that \(k\) ... basic algebra
+   7. \(n^2 = 2(2k^2) = 2k'\) for some integer \(k\) ... from 5, 6 (modus ponens)
+   8. if \(n^2 = 2(2k^2)\) for some integer \(k\), then \(n^2 = 2k'\) for some integer \(k'\) ... basic fact about integers
+   9. \(n^2 = 2k'\) for some integer \(k'\) ... from 7, 8 (modus ponens)
+   10. if \(n^2 = 2k'\) for some integer \(k'\), then \(n^2\) is even ... definition of even
+   11. \(n^2\) is even ... from 9, 10 (modus ponens)

(The “basic fact about integers” referred to above is that the product of integers is again an integer.) Since \(n\) could be replaced by any integer throughout this argument, we have proved the statement “if \(n\) is even then \(n^2\) is even” is true for all integers \(n\). (You might worry that the argument is only valid for even \(n\); see the disclaimer about Keanu Reeves’ acting ability on page 34, or remind yourself that \(P(n) \rightarrow Q(n)\) is automatically true if \(P(n)\) is false.) \(\blacksquare\)

Mathematical proofs are rarely presented with this degree of detail and formality. A slightly less formal proof of our proposition might leave out the explicit implications and instances of modus ponens and appear as follows:

Proof. Let \(n\) be an arbitrary integer.