**3.2** See the answer below:

```
x = x + 1;
x += 1;
++x;
x++;
```

**3.3** See the answers below:

+   a) product *= 2;
+   b) product = product * 2;
+   c) if (count > 10) {
+          puts("Count is greater than 10.");
+      }
+   d) quotient %= divisor;
+      quotient = quotient % divisor;
+   e) printf("%.2f", 123.4567);
+      123.46 is displayed.
+   f) printf("%.3f\n", 3.14159);
+      3.142 is displayed.

**3.4** See the answers below:

+   a) int x = 1;
+   b) int sum = 0;
+   c) sum += x; or sum = sum + x;
+   d) printf("The sum is: %d\n", sum);

**3.5** See below.

```
1  // Calculate the sum of the integers from 1 to 10
2  #include <stdio.h>
3
4  int main(void) {
5      int x = 1; // set x
6      int sum = 0; // set sum
7
8      while (x <= 10) { // loop while x is less than or equal to 10
9          sum += x; // add x to sum
10         ++x; // increment x
11     } // end while
12
13     printf("The sum is: %d\n", sum); // display sum
14 } // end main function
```

**3.6** See the answers below:

+   a) scanf("%d", &x);
+   b) scanf("%d", &y);
+   c) i = 1;
+   d) power = 1;
+   e) power *= x;
+   f) ++i;