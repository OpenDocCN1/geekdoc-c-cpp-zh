# 8.2. The while Loop

)
return 0;

The loop continues as long as i is less than or equal to 10. In each iteration, it prints the value of i and increments i by 1. The loop stops when i is greater than 10.

# Snippet: Factorial of a number

```
int n, i, fact = 1;

while (n > 0) {
    fact *= n;
    n--;
}
printf("%d", fact);
```

This loop calculates the factorial of a number n. The loop continues as long as n is greater than 0. Within each iteration, the current value of fact is multiplied by the current value of n, and the result is stored in fact. Then, n is decremented by 1. After the loop terminates, the calculated factorial value is printed. Note that n should be initialized to a specific value before the loop.

# Snippet: Greatest Common Denominator

The Greatest Common Denominator (GCD) is the largest positive integer that divides two or more numbers without leaving a remainder.

```
int a = 12;
int b = 15;

while (a != b) {
    if (a > b)
        a -= b;
    else
        b -= a;
}
printf("The GCD of 12 and 15 is %d\n", a);
```

This snippet uses the Euclidean algorithm, which is a well-known method for computing the GCD of two integers. The basic idea is to repeatedly subtract the smaller number from the larger number until the smaller number is 0. The last non-zero remainder is the GCD.

A more efficient version uses modulo:

```
int a = 12;
int b = 15;

while (a != b) {
```