```
```cpp
using namespace std;

int main()
{
   unsigned int sum = 0; // stores sum of integers 1 to 10
   unsigned int x = 1; // counter

   while ( x <= 10 ) // loop 10 times
   {
      sum += x; // add x to sum
      ++x; // increment x
   } // end while

   cout << "The sum is: " << sum << endl;
} // end main
```
```

```
```text
The sum is: 55
```
```

+   4.6
+      a) product = 25, x = 6;
+      b) quotient = 0, x = 6;

+   4.7
+      a) cin >> x;
+      b) cin >> y;
+      c) unsigned int i = 1;
+      d) unsigned int power = 1;
+      e) power *= x;
+         or
+         power = power * x;
+      f) ++i;
+      g) if (i <= y)
+      h) cout << power << endl;

4.8  See the following code:

```
```cpp
// Exercise 4.8 Solution: ex04_08.cpp
// Raise x to the y power.
#include <iostream>
using namespace std;

int main()
{
   unsigned int i = 1; // initialize i to begin counting from 1
   unsigned int power = 1; // initialize power

   cout << "Enter base as an integer: "; // prompt for base
   unsigned int x; // base
   cin >> x; // input base

   cout << "Enter exponent as an integer: "; // prompt for exponent
   unsigned int y; // exponent
   cin >> y; // input exponent

   // count from 1 to y and multiply power by x each time
   while (i <= y )
   {
      power *= x;
      ++i;
   } // end while
```
```