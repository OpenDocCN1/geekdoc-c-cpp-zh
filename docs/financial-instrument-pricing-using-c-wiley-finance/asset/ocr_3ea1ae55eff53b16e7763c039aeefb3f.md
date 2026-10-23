There is also an explicit formula for the nth Fibonacci number:

Fₙ = 1/√5 [αⁿ − βⁿ] where α = (1 + √5)/2, β = (1 − √5)/2. (12.4)

Using Pascal’s triangle we can compute the nth Fibonacci number by summing the elements in consecutive rows starting with row n. The corresponding code is:

```
// Fibonacci numbers by 'shallow' diagonals
std::size_t N = 4;    // Fib(N)
std::size_t i = 0;    // Running total
double val = 0.0;
for (std::size_t n = N; n >= i; --n)
{
    val += pascalTriangle(n,i);
    i++;
}
std::cout << N << "th Fibonacci number is: " << val;
```

Now define the sequence of numbers by:

xₙ = Fₙ / Fₙ₋₁,  n ≥ 1.

Then, by using equation (12.4) we can show that:

limₙ→∞ xₙ = α = (1 + √5)/2 (the Golden Ratio).

Fibonacci numbers have many applications, for example in single-variable optimisation in an interval using the methods Fibonacci search and Golden-Mean search for unimodal functions (Bronson and Naadimuthu, 1997). A unimodal function is one that has only one local minimum or local maximum in an interval. We discuss these minimisation algorithms in Chapter 19.

# 12.2.5 Triangular Numbers

The final example relating to Pascal’s triangle is to locate its triangular numbers. In general, the nth triangular numbers are formed by traversing down the triangle parallel to the right side of the triangle. For example, the code for the third triangular numbers is:

```
// 'Diagonal' elements of triangle
std::size_t row = 3; // The 3rd triangular numbers start
std::size_t k = 0;
for (std::size_t n=row;n <= pascalTriangle.MaxIndex(); ++n)
{
    std::cout << pascalTriangle(n,k++) << ", ";
}
```