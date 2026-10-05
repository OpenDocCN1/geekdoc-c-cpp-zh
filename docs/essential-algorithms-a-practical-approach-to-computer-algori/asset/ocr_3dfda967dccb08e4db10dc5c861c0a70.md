# Chapter 2 Numerical Algorithms 39

> **NOTE** This prime factoring algorithm has run time O(sqrt(N)), where N is the number it is factoring, so it is reasonably fast for relatively small numbers. If N gets large, O(sqrt(N)) isn't fast enough. For example, if N is 100 digits long, sqrt(N) has 50 digits. If N happens to be prime, even a fast computer won't be able to all the possible factors in a reasonable amount of time. This is what makes some cryptographic algorithms secure.

# Finding Primes

Suppose your program needs to pick a large prime number. (Yet another task required by some cryptographic algorithms.) One way to find prime numbers is to use the algorithm described in the preceding section to test a bunch of numbers to see if they are prime. For relatively small numbers, that works, but for very large numbers, it can be prohibitively slow.

The sieve of Eratosthenes is a simple method of finding all the primes up to a limit. This method works well for relatively small numbers, but it requires a table with every number that is considered. Therefore, it uses unreasonable amount of memory if the numbers are too large.

The basic idea is to make a table with one entry for each number between 2 and the upper limit. Cross out all the multiples of 2 (not counting 2 itself). Then, starting at 2, look through the table to find the next number that is not crossed (3 in this case). Cross out all multiples of that value (not counting the value itself). Note that some of value may already be crossed out because they were also multiples of 2. Repeat this step, finding the next value that is not crossed, and cross out its multiples until you reach the square root of the upper limit. At any point, any numbers that are not crossed are prime.

The following pseudocode shows the basic algorithm:

```
// Find the primes between 2 and max_number (inclusive).
List Of Integer: FindPrimes(long max_number)
// Allocate an array for the numbers.
Boolean: is_composite = new bool[max_number + 1]

// Cross out multiples of 2.
For i = 4 to max_number Step 2
    is_composite[i] = true
Next i

// Cross out multiples of prime found so far.
Integer: next_prime = 3
Integer: stop_at = Sqrt(max_number)
While (next_prime < stop_at)
    // Cross out" multiples of this prime.
    For i = next_prime * 2 To max_number Step next_prime Then
        is_composite[i] = true
Next i
```