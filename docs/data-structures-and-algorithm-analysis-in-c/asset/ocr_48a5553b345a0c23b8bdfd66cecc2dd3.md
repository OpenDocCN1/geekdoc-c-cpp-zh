| Function | Name |
|---|---|
| c | Constant |
| log N | Logarithmic |
| log<sup>2</sup> N | Log-squared |
| N | Linear |
| N log N | |
| N<sup>2</sup> | Quadratic |
| N<sup>3</sup> | Cubic |
| 2<sup>N</sup> | Exponential |

# Figure 2.1 Typical growth rates

**Rule 3**
log<sup>k</sup> N = O(N) for any constant k. This tells us that logarithms grow very slowly.

This information is sufficient to arrange most of the common functions by growth rate (see Fig. 2.1).

Several points are in order. First, it is very bad style to include constants or low-order terms inside a Big-Oh. Do not say T(N) = O(2N<sup>2</sup>) or T(N) = O(N<sup>2</sup> + N). In both cases, the correct form is T(N) = O(N<sup>2</sup>). This means that in any analysis that will require a Big-Oh answer, all sorts of shortcuts are possible. Lower-order terms can generally be ignored, and constants can be thrown away. Considerably less precision is required in these cases.

Second, we can always determine the relative growth rates of two functions f(N) and g(N) by computing lim<sub>N→∞</sub> f(N)/g(N), using l'Hôpital's rule if necessary:<sup>1</sup> The limit can have four possible values:

+   * The limit is 0: This means that f(N) = o(g(N)).
+   * The limit is c ≠ 0: This means that f(N) = Θ(g(N)).
+   * The limit is ∞: This means that g(N) = o(f(N)).
+   * The limit does not exist: There is no relation (this will not happen in our context).

Using this method almost always amounts to overkill. Usually the relation between f(N) and g(N) can be derived by simple algebra. For instance, if f(N) = N log N and g(N) = N<sup>1.5</sup>, then to decide which of f(N) and g(N) grows faster, one really needs to determine which of log N and N<sup>0.5</sup> grows faster. This is like determining which of log<sup>2</sup> N or N grows faster. This is a simple problem, because it is already known that N grows faster than any power of a log. Thus, g(N) grows faster than f(N).

One stylistic note: It is bad to say f(N) <= O(g(N)), because the inequality is implied by the definition. It is wrong to write f(N) >= Ω(g(N)), because it does not make sense.

<sup>1</sup> l'Hôpital's rule states that if lim<sub>x→∞</sub> f(x) = ∞ and lim<sub>x→∞</sub> g(x) = ∞, then lim<sub>x→∞</sub> f(x)/g(x) = lim<sub>x→∞</sub> f'(x)/g'(x), where f'(x) and g'(x) are the derivatives of f(x) and g(x), respectively