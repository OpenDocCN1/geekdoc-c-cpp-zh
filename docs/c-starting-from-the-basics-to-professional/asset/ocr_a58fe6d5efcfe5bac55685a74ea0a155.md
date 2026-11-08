All the work is done in two loops: the outer while loop picks the next candidate to be checked and adds the candidate to the primes array if it’s prime, and the inner loop checks the current candidate to see whether it’s prime. The outer loop continues until the primes array is full.

The algorithm in the loop that checks for a prime is simple. It’s based on the fact that any number that isn’t a prime must be divisible by a smaller number that is a prime. You find the primes in ascending order, so at any point primes contains all the prime numbers lower than the current candidate. If none of the values in primes is a divisor of the candidate, then the candidate must be prime. Once you realize this, writing the inner loop that checks whether trial is prime should be straightforward:

```
```c
// Try dividing the candidate by all the primes we have
for (size_t i {}; i < count && isprime; ++i)
{
    isprime = trial % *(primes + i) > 0;  // False for exact division
}
```
```

In each iteration, isprime is set to the value of the expression trial % *(primes + i) > 0. This finds the remainder after dividing trial by the number stored at the address primes + i. If the remainder is positive, the expression is true. The loop ends if i reaches count or whenever isprime is false. If any of the primes in the primes array divides into trial exactly, trial isn’t prime, so this ends the loop. If none of the primes divides into trial exactly, isprime will always be true, and the loop will be ended by i reaching count.

> **Note**  Technically you only need to try dividing by primes that are less than or equal to the square root of the number in question, so the example isn’t as efficient as it might be.

After the inner loop ends, either because isprime was set to false or because the set of divisors in the primes array has been exhausted, whether or not the value in trial was prime is indicated by the value in isprime. This is tested in an if statement:

```
```c
if (isprime)
{
    *(primes + count++) = trial;      // We got one...
                                     // ...so save it in primes array
}
```
```

If isprime contains false, then one of the divisions was exact, so trial isn’t prime. If isprime is true, the assignment statement stores the value from trial in primes[count] and then increments count with the postfix increment operator. When max primes have been found, the outer while loop ends, and the primes are output to a line with a field width of seven characters as a result of these statements in a for loop.

# Dynamic Memory Allocation

Most code you’ve written up to now allocates space for data at compile time. The most notable exceptions are the times when you used a std::vector<> container, which dynamically allocates and any memory it needs to hold its elements. Apart from that, you’ve mostly specified all variables and arrays that you needed in the code up front, and that’s what will be allocated when the program starts, whether you need the entire array or not. Working with a fixed set of variables in a program can be very restrictive, and it’s often wasteful.