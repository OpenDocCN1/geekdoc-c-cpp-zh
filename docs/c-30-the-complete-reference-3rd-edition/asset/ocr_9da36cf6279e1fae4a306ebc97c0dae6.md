```
} else Console.WriteLine(i + " is not prime.");
}
```

Here is the output produced by the program:

```
2 is prime.
3 is prime.
4 is not prime.
5 is prime.
6 is not prime.
7 is prime.
8 is not prime.
9 is not prime.
```

In the program, IsPrime() is called nine times, and each time a different value is passed. Let's look at this process closely. First, notice how IsPrime() is called. The argument is specified between the parentheses. When IsPrime() is called the first time, it is passed value 1. Thus, when IsPrime() begins executing, the parameter x receives the value 1. In the second call, 2 is the argument, and x then has the value 2. In the third call, the argument is 3, which is the value that x receives, and so on. The point is that the value passed as an argument when IsPrime() is called is the value received by its parameter, x.

A method can have more than one parameter. Simply declare each parameter, separating one from the next with a comma. For example, here the ChkNum class is expanded by adding a method called LeastComFactor(), which returns the smallest factor that its two arguments have in common. In other words, it returns the smallest whole number value that can evenly divide both arguments.

```
// Add a method that takes two arguments.

using System;

class ChkNum {
    // Return true if x is prime.
    public bool IsPrime(int x) {
        if(x <= 1) return false;

        for(int i=2; i <= x/2; i++)
            if((x %i) == 0) return false;

        return true;
    }

    // Return the least common factor.
    public int LeastComFactor(int a, int b) {
        int max;

        if(IsPrime(a) || IsPrime(b)) return 1;

        max = a < b ? a : b;

        for(int i=2; i <= max/2; i++)
            if(((a%i) == 0) && ((b%i) == 0)) return i;
```