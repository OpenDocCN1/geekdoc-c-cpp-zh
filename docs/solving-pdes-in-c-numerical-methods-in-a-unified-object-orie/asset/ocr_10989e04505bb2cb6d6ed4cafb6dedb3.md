looks at its concrete argument. If it is a polynomial of one variable, then the previous version is invoked. If, on the other hand, it is a polynomial of two variables, then this version is invoked.

# 5.15 Application in Cryptography

A decimal number may also be considered as a polynomial in 10. After all, the rightmost (unit) digit is just a multiple of 10⁰ = 1, the next digit to its left is a multiple of 10¹ = 10, and so on. In elementary (primary) school, we learn how to do long arithmetic operations. What we are not told is that these operations are actually based on mathematical induction: we assume that the algorithm works well for numbers with n digits (or columns), and then we extend the algorithm to slightly larger numbers with n + 1 digits as well. This is indeed easy to do: once the technique is applied to the first column, we are left with a shorter number of n digits only, for which we have assumed that the algorithm works fine. So, we apply the original algorithm recursively to this shorter number of n digits, which we already know how to do, and so on, until we get to the final column and conclude.

Then, we have to make sure that there is no error. For this purpose, we apply the inverse arithmetic operation to our result: if the original exercise is division, then the inverse operation is multiplication. Once this check is successful, we know that we made no error.

The principle of mathematical induction guarantees that long operations apply to arbitrarily long numbers with n as large as we like. This is useful, for example, to produce practically unbreakable codes to transfer secret messages over the internet. This is indeed done below.

For this purpose, the object-oriented approach turns out to be particularly helpful. Furthermore, the implementation turns out to be particularly short and elegant with binary (rather than decimal) representation of integer numbers.

# 5.16 Finding Prime Numbers

In the sequel, we study a few algorithms for practical problems in cryptography. The algorithms are then implemented in the present object-oriented framework.

Consider the problem of finding all the prime numbers that lie between 2 and a given large integer number N. At first glance, it would make sense to solve this problem inductively: assume that we have already found all the prime numbers that are smaller than a given number n and stored them (in increasing order) in a linked list. We could then find out whether n is prime or not by scanning this linked list and checking whether n is divided evenly by any of the numbers in it.

Note that only prime numbers whose square is not larger than n must be checked to see whether or not they divide n evenly. After all, if some prime number p > √n divides n evenly, then there must be a number q ≤ √n such that n = p q. In this case, n must have already been proved to be nonprime long ago, as it is divided evenly also by each prime factor of q.

The "isPrime" function below returns a Boolean variable of type "bool" that can take the value zero or one only:

```
template<class T>
bool isPrime(const T&n, const linkedList<T>& primes) {
```