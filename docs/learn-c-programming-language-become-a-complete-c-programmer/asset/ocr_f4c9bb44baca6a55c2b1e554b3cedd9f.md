generality at the cost of performance.

The experienced programmer will note that sum() can be generalized further. In particular, the use of an extra template argument is awkward, and we required the initial value 0. We can solve that by letting the caller supply an initial value and then deduce Val:

```
template<typename Iter, typename Val> Val accumulate(Iter first, Iter last, Val s) {
while ( first!=last) { s=s+ *first; ++first;
}
return s;
}
```

```
double ad[] = {1,2,3,4};
double s1 = accumulate(ad,ad+4,0.0); double s2 = accumulate(ad,ad+4,0);
```

// accumulate in a double // accumulate in an int

But why +? We sometimes want to multiply elements. In fact, there seem to be quite a few operations we might want to apply to the elements of a sequence. This leads to a further generalization:

```
template<typename Iter, typename Val, typename Oper>
Val accumulate(Iter first, Iter last, Val s, Oper op)
{
while ( first!=last) { s = op(s,*first); ++first;
}
return s;
}
```

We now use the argument op to combine element values with the accumulator. For example:

```
double ad[] = {1,2,3,4};
double s1 = accumulate(ad,ad+4,0.0,std::plus<double>); // as before
double s2 = accumulate(ad,ad+4,1.0,std::multiply<double>);
```

The standard library provides common operations, such as plus and multiply, as function objects to be used as arguments. Here, we see the utility of having the caller supply the initial value: 0 and * don’t go well together for accumulation. The standard library offers a further generalization of accumulate() that allows a user to provide an alternative to = for combining the result of the “addition” and the accumulator (§40.6).

Lifting is a skill that requires knowledge of an application domain and some experience. The most important single guide for designing algorithms is to lift them from concrete examples without adding features (notation or run-time cost) that would impair their use. The standard-library algorithms are the results of lifting done with great attention to performance issues.

# 24.3 Concepts