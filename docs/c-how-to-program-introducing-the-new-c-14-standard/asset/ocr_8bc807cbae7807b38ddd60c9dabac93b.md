23 expresses the problem as the product of `number` and a *recursive* call to `factorial` evaluating the factorial of `number - 1`, which is a slightly *simpler* problem than the original calculation `factorial(number)`.

```
// Fig. 6.25: fig06_25.cpp
// Recursive function factorial.
#include <iostream>
#include <iomanip>
using namespace std;

unsigned long factorial(unsigned long); // function prototype

int main() {
   // calculate the factorials of 0 through 10
   for (unsigned int counter{0}; counter <= 10; ++counter) {
      cout << setw(2) << counter << "! = " << factorial(counter)
           << endl;
   }
}

// recursive definition of function factorial
unsigned long factorial(unsigned long number) {
   if (number <= 1) { // test for base case
      return 1; // base case: 0! = 1 and 1! = 1
   }
   else { // recursion step
      return number * factorial(number - 1);
   }
}
```

```
0! = 1
1! = 1
2! = 2
3! = 6
4! = 24
5! = 120
6! = 720
7! = 5040
8! = 40320
9! = 362880
10! = 3628800
```

Fig. 6.25 Recursive function `factorial`.