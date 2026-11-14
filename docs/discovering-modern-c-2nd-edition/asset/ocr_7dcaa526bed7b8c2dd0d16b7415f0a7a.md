```
{
    return sin(x) + cos(x);
}
int main() {
    cout << fin_diff(sin_plus_cos, 1., 0.001) << '\n';
    cout << fin_diff(sin_plus_cos, 0., 0.001) << '\n';
}
```

Here we approximated the derivative of `sin_plus_cos` at `x = 1` and `x = 0` with `h = 0.001`. `sin_plus_cos` is passed as a function pointer (functions can be implicitly converted to function pointers when necessary).

Now we want to compute the second-order derivative. It would make sense to call `fin_diff` with itself as an argument. Unfortunately, this is not possible since `fin_diff` has three parameters and does not match its own function pointer parameter for unary functions. We can solve this problem with:

# **Definition 3–2.** *Functors* are classes that provide an application `operator()` so that objects thereof can be called like functions.

Some other authors use the term “function object” instead of functor and unfortunately it is often not obvious in their texts whether they refer to a class or to an object. This might not be problematic in those contexts but we need the sharp distinction between classes and objects here. Therefore we prefer the word *functor* despite its other meaning in category theory. In this book, a functor always refers to a class and an object thereof is accordingly called a functor object. The term *Function Object* we use for all objects that can be called like a function. This can be a regular function, a functor object, a lambda (next section), or a function pointer.

Back to our example. The previously used function `sin_plus_cos` implemented as a functor reads as follows:

# **Listing 3–6: Functor**

Click here to view code image

```
struct sc_f
{
    double operator()() (double x) const
```