```
if ( result == 0) // prime
{
    printf("%d ", idx);
}
}

return 0;
}
```

Listing 4.10 contains the function isPrime() that returns 0 if a number is prime and returns 1 if a number is composite. The isPrime() function contains a for loop that starts at 2 and ends at idx /2, and checks whether or not any of these numbers are divisors of the number idx. If so, then the flag variable (which is initialized with the value 0) is set to 1 and the code exits the loop; otherwise the loop terminates normally. In either case, the isPrime() function returns the value of flag.

Next, the body of the main() function contains a for loop whose loop variable idx iterates from 1 to maxVal (which is initialized as 50). Each iteration through the for loop invokes the isPrime() function with the current value of idx. The next portion of the for loop prints the value of idx only if idx is prime (i.e., isPrime() returns a 0).

The output from Listing 4.10 is here:
1 2 3 5 7 11 13 17 19 23 29 31 37 41 43 47

This concludes the discussion of custom functions in C programs. The next portion of this chapter introduces you to recursion, along with some code samples that illustrate how to use recursion in C.

# WHAT IS RECURSION?