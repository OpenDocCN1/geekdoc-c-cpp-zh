As a demonstration of what I mean, let’s use a time-honored example taken from Knuth’s wonderful book *Literate Programming*.¹ Listing 10-5 shows a translation into Java of Knuth’s `PrintPrimes` program. To be fair to Knuth, this is not the program as he wrote it but rather as it was output by his WEB tool. I’m using it because it makes a great starting place for breaking up a big function into many smaller functions and classes.

# **Listing 10-5** `PrintPrimes.java`

```
```java
package literatePrimes;

public class PrintPrimes {
  public static void main(String[] args) {
    final int M = 1000;
    final int RR = 50;
    final int CC = 4;
    final int WW = 10;
    final int ORDMAX = 30;
    int P[] = new int[M + 1];
    int PAGENUMBER;
    int PAGEOFFSET;
    int ROWOFFSET;
    int C;

    int J;
    int K;
    boolean JPRIME;
    int ORD;
    int SQUARE;
    int N;
    int MULT[] = new int[ORDMAX + 1];

    J = 1;
    K = 1;
    P[1] = 2;
    ORD = 2;
    SQUARE = 9;
```
```