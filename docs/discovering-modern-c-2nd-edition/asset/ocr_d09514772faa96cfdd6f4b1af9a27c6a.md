```
auto l= [&r= x, i= x + 1]{ r+= 2; return i + 1; };
```

The most important benefit of this generalization is (for us) the ability to move variables into a closure. Say we have a function returning a Hilbert matrix as `unique_ptr`:

```
auto F= make_unique<Mat>(Mat({1., 0.5} ,{0.5,1./3.}));
```

We are allowed to capture `F` as reference which unfortunately would turn stale when the closure outlives the pointer. On the other hand, a `unique_ptr` cannot be copied. For assuring that our matrix exists as long as the closure, we have to move the data into a `unique_ptr` owned by the closure:

```
auto apply_f= [F= move(F)](const Vec& x){ return Vec(*F * x); };
```

We need this moving ability for instance when a function shall return a lambda that captures a local variable of a non-copyable type.

# ## 3.8.2 Generic Lambdas

C++14 Lambdas in C++11 determined the return type but the arguments needed to be declared explicitly. This restriction was lifted in C++14. In contrast to function templates, the arguments are not declared in the somewhat verbose template-typename notation but by the keyword `auto`. For instance, a function that sorts elements of a (random-access) container in descending order is implemented as simply as:

Click here to view code image

```
template <typename C>
void reverse_sort(C& c)
{
    sort(begin(c), end(c), [](auto x, auto y){ return x > y;
    });
}
```

In the same fashion, we can simplify our `frobenius_norm` from Section 3.8.1.2. The lambda summing the squared magnitudes can simply instantiate the argument type:

Click here to view code image