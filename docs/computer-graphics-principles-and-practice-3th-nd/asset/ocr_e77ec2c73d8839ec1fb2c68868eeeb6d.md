# ## 7.4 Functions

The notion of a *function* is already familiar to you from both mathematics and programming. We’ll use a particular notation to express functions; an example is

$$ f : \mathbf{R} \to \mathbf{R} : x \mapsto x^2. \qquad (7.7) $$

The name of the function is $f$. Following the colon are two sets. The one to the left of the arrow is called the *domain*; the one to the right is called the *codomain* (some books use the term “range” for this; however, “range” is also used in a similar but different sense, leading to confusion). Following the second colon is a description of the rule for associating to an element of the domain, $x$, an element of the codomain.

This corresponds closely to the definition of a function in many programming languages, which tends to look like this:

```
```c
double f(double x)
{
    return x * x;
}
```
```

Once again, the function is named; the domain is explicitly defined (“$x$ can be any double”), and the codomain is explicitly defined (“this function produces doubles”). The rule for associating the typical domain element, $x$, with the resultant value is given in the body of the function.

Mathematics allows somewhat subtler definitions than do most programming languages. For example, we can define

$$ g : \mathbf{R} \to \mathbf{R}_0^+ : x \mapsto x^2 \qquad (7.8) $$

in mathematics, but most languages lack a data type which is a “non-negative real number.” The distinction between $f$ and $g$ is important, however: In the case of $g$ the set of values produced by the function (i.e., the set $\{x^2 : x \in \mathbf{R}\}$) turns out to be the entire codomain, while in $f$ it is a proper subset of the codomain. The function $g$ is said to be *surjective*, while $f$ is not. (Some books say that “$g$ is onto.”)

If we define

$$ h : \mathbf{R}_0^+ \to \mathbf{R}_0^+ : x \mapsto x^2, \qquad (7.9) $$

we get yet a different function. The function $h$ is not only surjective, it has another property: No two elements of the domain correspond to the same element of the codomain; that is, if $h(a) = h(b)$, then $a$ and $b$ must be equal. Such a function is called *injective*.^2 A function like $h$ that’s both injective and surjective has an *inverse*, denoted $h^{-1}$, a function that “undoes” what $h$ does. The domain of $h^{-1}$ is the codomain of $h$, and vice versa. In the case of our particular function, the inverse is

$$ h^{-1} : \mathbf{R}_0^+ \to \mathbf{R}_0^+ : x \mapsto \sqrt{x}. \qquad (7.10) $$

2. Some books use the term “one-one” or “one-to-one,” but others use the same term to mean both injective and surjective.