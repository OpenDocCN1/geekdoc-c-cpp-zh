that the tree centres around the strike price. The method is an improvement on other methods such as CRR because of the less jagged convergence properties. The up and down parameters are defined by (Haug, 2007, pp. 290–292):

$$u=e^{b\Delta t}\frac{h(d_1)}{h(d_2)},\quad d=\frac{e^{b\Delta t}-pu}{1-p},\quad p=h(d_2)$$  \tag{11.6}

where:

$$b=\text{cost-of-carry}$$

$$\Delta t=T/NT$$

$$d_1=\frac{\log(S/K)+(b+\sigma^2/2)T}{\sigma\sqrt{T}}$$

$$d_2=d_1-\sigma\sqrt{T}.$$

Finally, $h=h(x)$ is a specially chosen function, for example the Preitzer–Pratt inversion formula. Details can be found in Haug (2007).

# 10. (Code Reduction Using Variadic Parameters)

The algorithms for forward and backward induction in Layer 2 of the software framework use tuples. In particular, binomial lattices use tuples with two components while trinomial lattices use tuples with three components. The current design leads to duplicate code and we would like to create a single algorithm for forward induction and a single algorithm for backward induction. This goal should be achievable by using the fact that the second template parameter in the Level 1 lattice class tells us how many components to use as output (in the case of forward induction) or as input (in the case of backward induction). For example, we could use a fixed-size array std::array<T,N> where N = 2 for binomial lattices and N = 3 for trinomial lattices or the more exotic case of variadic templates in a later version.

We implement the algorithms for forward and backward induction for plain options using std::array<T,N> instead of std::tuple<>. To motivate what we mean, we give the function prototype and code of the forward induction algorithm:

```
template <typename Node, int LatticeType> void ForwardInduction
    (Lattice<Node, LatticeType>& lattice, const std::function
    <std::array<Node, LatticeType>
    (const Node& node)>& generator, const Node& rootValue)

{
    // Initialise the root value lattice[0][0]
    std::size_t si = lattice.MinIndex();
    lattice[si][0] = rootValue;

    std::array<Node, LatticeType> tuple;

    // Loop from min index to end index, i.e. (min, end]
    for (std::size_t n = lattice.MinIndex() + 1;
```