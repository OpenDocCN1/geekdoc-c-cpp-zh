sin x = x - \frac{x^3}{6} \quad (2.5.3)

but the Taylor series centered about \( x = \pi \) is given by

sin x = \pi \frac{\pi^3}{6} + \left( \frac{\pi^2}{2} - 1 \right) x - \frac{\pi}{2} x^2 + \frac{1}{6} x^3 \\ = \pi - \frac{\pi^3}{6} + x \left( \left( \frac{\pi^2}{2} - 1 \right) - x \left( \frac{\pi}{2} + \frac{1}{6} \right) \right) \quad (2.5.4)

The latter in Horner form has more terms than the previous, and thus although the error is smaller in the second case but still comparable, the first approximation is better since it involves less computational complexity. If we were to add more terms to the first approximation such that it would match the number of terms of the second approximation, the first approximation would provide a smaller error for the same number of terms and thus would be deemed a better approximation than the latter.

sin x = x \left( 1 - \frac{x^2}{6} \right) \quad (2.5.5)

More generally, \( x^2 \) can be factored out for any degree, significantly reducing the computational complexity for a given precision since the MacLaurin approximation of the sine function has a coefficient of zero for all terms of even degree. Consequently, it is not only important to look at how a given function approximates another one very well, it is also important to look at the computational complexity. This makes it easier to speak of the best approximation as the function over that for a given degree of multi-applicative complexity minimizes the maximum error over an interval \( [a,b] \).

# Introducing the Minimax Approximation

Now that we have defined the properties for “the best approximation” as far as we are concerned, we can define minimax approximation. The minimax approximation is the best approximation for a given polynomial degree. It has no relation or knowledge of computational complexity (i.e., how much work it takes to compute) and thus differs a little bit from our definition of best approximation. Consequently for our purposes, in a single line, the minimax approximation is a polynomial approximation of degree \( n \) that minimizes the maximum error of a given function. By construction, the minimax approximation is the holy grail of approximation for a given polynomial degree, and it is unique up to permutations of equivalent equations. Because it has no knowledge of complexity, it should be noted that some other approximations could sometimes yield “better approximations.” In other words, for the same degree, the minimax approximation will still be better or equal to the better approximation, but