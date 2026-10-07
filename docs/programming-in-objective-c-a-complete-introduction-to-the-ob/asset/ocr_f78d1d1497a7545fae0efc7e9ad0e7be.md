# Chapter 6 Making Decisions

```
...
case '*':
case 'x':
  [deskCalc multiply:value2];
  break;
}
```

# Boolean Variables

Just about anyone learning to program soon faces the task of having to write a program to generate a table of prime numbers. To refresh your memory, a positive integer, p, is a prime number if it is not divisible by any other integers than 1 and itself. The first prime integer is defined to be 2. The next prime is 3 because it is not divisible by any integers other than 1 and a is not prime because it is even.

You can take several approaches to generate a table of prime numbers. If you had the task of generating all numbers up to 50, the most straightforward (and simplest) algorithm to generate such a table would test every integer, p, for divisibility by all integers from 2 through p-1. If any such integer divided by p, then p would not be prime; otherwise, it would be a prime number. Program 6.10 generates a list of prime numbers from 2 to 50.

Program 6.10

```
// Program to generate a table of prime numbers

#import <Foundation/Foundation.h>
int main (int argc, char *argv[]) {
  NSAutoreleasePool *pool = [NSAutoreleasePool alloc];

  int p, d, isPrime;

  for ( p = 2; p <= 50; ++p) {
    isPrime = 1;

    for ( d = 2; d < p; ++d) {
      if (p % d == 0)
        isPrime = 0;
    }
  }

  if (isPrime != 0) {
    NSLog("@%i", p);
  }

  [pool drain];
  return 0;
}
```