# 5.7 Exercises

# 5.7.1 Type Traits

Write type traits for removing and adding references. Add a domain-specific type trait for the meta-predicate `is_vector` and assume that the only known vectors are so far `my_vector<Value>` and `vector_sum<E1, E2>`.

# 5.7.2 Fibonacci Sequence

Write a template meta-function that computes the \(n^{\text{th}}\) value of the Fibonacci sequence at compile time. The Fibonacci sequence is defined by the following recursion:

```
x_0 = 0
x_1 = 1
x_n = x_{n-1} + x_{n-2} \text{ for } n \ge 2.
```

# 5.7.3 Meta-Program for Greatest Common Divisor

Write a meta-program for the GCD (greatest common divisor) of two integers. The algorithm is as follows:

Click here to view code image

```
1 function gcd(a, b):
2     if b = 0 return a
3     else return gcd(b, a mod b)
```

Click here to view code image

```
template <typename I>
I gcd( I a, I b ) { ... }
```

Then write an integral meta-function that executes the same algorithm but at compile time. Your meta-function should be of the following form:

Click here to view code image

```
template <int A, int B>
struct gcd_meta {
```