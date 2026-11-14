calculate every Turing-computable function, i.e., every function describable by an algorithm.

# Theorem

The meta-programming of C++ is Turing-complete.

We will prove that in this section. Todd Veldhuizen demonstrated this before by implementing a Turing machine with traditional templates [71]. This proved that the template system is Turing-complete. We have chosen another way by illustrating that `constexpr` functions model \(\mu\)-recursive functions. The notation is used from Lutz Hamel's lecture on “Theory of Computation” [29].

First we show that all \(\mu\)-recursive functions can be implemented with `constexpr` functions:

# **Zero Functions** map from arbitrary arguments to zero:

\(f^k(n_1, ..., n_k) := 0\)

Considering for instance three arguments we can easily implement:

Click here to view code image

```
```cpp
constexpr int ternary_zero(int, int, int)
{
    return 0;
}
```
```

# **Projection on Argument** returns one of the arguments:

\(\pi_i^k (n_1, ..., n_k) := n_i\)

An exemplary implementation for returning the second of three arguments is:

Click here to view code image

```
```cpp
constexpr int second_from_three(int, int j, int)
{
    return j;
}
```
```