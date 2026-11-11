optimization level in the C++ compiler, it beats Java with a time of 14 milliseconds. Java could only match that if the program ran long enough to trigger the Hotspot just-in-time compiler.

# **Listing 9.8** `sieve/Sieve.java`

```
    1  package sieve;
    2
    3  import java.util.*;
    4
    5  /**
    6   * This program runs the Sieve of Eratosthenes benchmark.
    It computes all primes
    7   * up to 2,000,000.
    8   * @version 1.22 2021-06-17
    9   * @author Cay Horstmann
    10  */
    11 public class Sieve
    12 {
    13      public static void main(String[] s)
    14     {
    15         int n = 2000000;
    16         long start = System.currentTimeMillis();
    17         var bitSet = new BitSet(n + 1);
    18         int i;
    19         for (i = 2; i <= n; i++)
    20             bitSet.set(i);
    21         i = 2;
    22         while (i * i <= n)
    23         {
    24             if (bitSet.get(i))
    25             {
    26                 int k = i * i;
    27                 while (k <= n)
    28                 {
    29                     bitSet.clear(k);
    30                     k += i;
    31                 }
```