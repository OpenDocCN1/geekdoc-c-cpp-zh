```
```java
import java.io.*;
import java.util.*; // Scanner class is inside this package
import java.math.*; // BigInteger class is inside this package

class Main { /* Uva 10925 - Krakovia */
  public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    int caseNo = 1;
    while (true) {
      int N = sc.nextInt(), F = sc.nextInt(); // N bills, F friends
      if (N == 0 && F == 0) break;
      BigInteger sum = BigInteger.valueOf(0); // use valueOf to initialize
      for (int i = 0; i < N; i++) { // sum the N large bills
        BigInteger V = sc.nextBigInteger(); // for reading next BigInteger!
        sum = sum.add(V); // this is BigInteger addition
      }
      System.out.println("Bill #" + (caseNo++) + " costs " +
        sum + ": each friend should pay " + sum.divide(BigInteger.valueOf(F)));
      System.out.println(); // the line above is BigInteger division
    } } }                 // divide the large sum to F friends
```
```

# ### 5.4.2 Bonus Features

The Java BigInteger class has a few more bonus features that can be useful in programming contests. It happens to have a built-in GCD routine gcd(BI), a modular arithmetic function modPow(BI exponent, BI m), and Base Number converter toString(int radix).

# ### GCD Revisited

When we need to compute the GCD of two big integers, we do not have to worry. See an example below for UVa 10814 - Simplifying Fractions that ask us to simplify a given (large) fraction to its simplest form by dividing both numerator and denominator with the gcd between them.

```
```java
import java.io.*;
import java.util.*;
import java.math.*;

class Main { /* Uva 10814 - Simplifying Fractions */
  public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    int N = sc.nextInt();
    while (N-- > 0) {
      BigInteger p = sc.nextBigInteger();
      String ch = sc.next(); // ignore this one
      BigInteger q = sc.nextBigInteger();
      BigInteger gcd_pq = p.gcd(q); // wow :)
      System.out.println(p.divide(gcd_pq) + " / " + q.divide(gcd_pq));
    } } }
```
```

# ### Modulo Arithmetic Revisited

One of the problems presented in the previous section is LA 4104 - MODEX. We are asked to find what is the value of x^y(mod n). It turns out that this problem can be solved with: