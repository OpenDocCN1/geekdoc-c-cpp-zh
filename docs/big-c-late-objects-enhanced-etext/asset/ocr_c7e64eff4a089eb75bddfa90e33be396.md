Finally, we would like to find out why the program believes 9 is a prime. Continue debugging until the breakpoint is hit with i = 9. Step into the isprime function. Now use “step over” repeatedly. The two if statements are skipped, which is correct since 9 is an odd number. The program again skips past the while loop. Inspect k to find out why. k is 3. Look at the condition in the while loop. It tests whether k * k < n. Now k * k is 9 and n is also 9, so the test fails.

When checking whether n is prime, it makes sense to only test divisors up to √n. If n can be factored as p × q, then the factors can't both be greater than √n. But actually that isn't quite true. If n is a perfect square of a prime, then its sole nontrivial divisor is equal to √n. That is exactly the case for 9 = 3 × 3. We should have tested for k * k <= n.

By running the debugger, we discovered three bugs in the program:

+   - isprime falsely claims 1 to be a prime.
+   - main doesn't test 2.
+   - There is an off-by-one error in isprime. The condition of the while statement should be k * k <= n.

Here is the improved program:

```
#include <iostream>

using namespace std;

/**
 * Tests if an integer is a prime.
 * @param n any positive integer
 * @return true if n is a prime, false otherwise
 */
bool isprime(int n)
{
    if (n == 1)
    {
        // 1 is not a prime
        return false;
    }
    if (n == 2)
    {
        // 2 is a prime
        return true;
    }
    if (n % 2 == 0)
    {
        // No other even number is a prime
        return false;
    }

    // Try finding a number that divides n

    int k = 3; // No need to divide by 2 since n is odd
    // Only need to try divisors up to sqrt(n)
    while (k * k <= n)
    {
        if (n % k == 0)
        {
            // n is not a prime since it is divisible by k
            return false;
        }
        // Try next odd number
        k = k + 2;
    }
}
```