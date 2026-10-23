```
void print(const Container<T, TAlloc>& container,
    const std::string& comment)
{ // A generic print function for general containers

    std::cout << comment << ": ";

    // TBD
}
```

9. (Examples of Complexity)
Verify the following:
17n^(1/6) ∈ O(n^(1/5))
10^6 n^2 ∈ O(n^2)
n log₂ n − 100 ∈ Ω(n).

10. (Calculating Orders of Complexity)
a) Let p(n) be any polynomial of degree n whose leading coefficient is positive and let a be any real number such that a > 1. Show that p(n) ∈ O(a^n).
b) Show that a^n ∈ O(b^n) if 1 < a < b.
c) Show that S(n, −k) ∈ Θ(1) for all integers k ≥ 2 where S(n, −k) = Σ_{j=1}^n (1/j)^k.

11. (Greatest Common Denominator (gcd) as a Recursive Function)
Implement and test a recursive function to compute the greatest common divisor gcd(m, n) of two positive integers. The code corresponding to this recursive function is given by:

```
int gcd(int m, int n)
{
    if (n == 0) return m;

    int rem = m%n;

    if (rem == 0) return n;

    return gcd(n, rem);
}
```

Answer the following questions:
a) Test the above code and compare your answers with another source, for example the Boost Math Common Factor library.
b) Write code to find the gcd of an array of integers. In Demming and Duffy (2010) we converted the array to a stack. We then pop two elements m and n from the stack, push gcd(m, n) onto the stack and repeat the process until there is only one element left on the stack. This value will be the gcd of the array.
c) How do you debug this recursive function?