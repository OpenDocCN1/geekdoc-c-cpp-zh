```
main()
{
int i; float k; char s[20];
printf("\nType a positive number: ");
gets(s); i=atoi(s);
k=Factori(i); printf("\n n!=%18.0f",k);
}
```

Modifications to exercise: The first change is on the type. The float declaration can be changed to int, in the function and in the variable k. Which are the advantages and disadvantages? The reader knows that with numbers declared as integers the program processing is done much faster. The problem is that only it is possible to calculate up to 7!, for 8! already result in a value greater than 40,000, outside the signalized integers range. Hence, unsigned int may be a preferred type. Or long. In each case, be sure to adjust the print format in printf(). The second amendment to be proposed is the change of the function, from factori() to Fib(). This Fib() function returns the nth Fibonacci sequence element. Fibonacci, or Leonardo of Pisa, was the greatest European mathematician of the Middle Age and among his inventions there is the sequence that takes its name: 1, 1, 2, 3, 5, 8, 13, ... The building rule is: each term is the sum of the previous two. We have: Fib(1) = 1; Fib(2) = 1; Fib(3) = fib(2) + fib(1), ..., fib(n) = fib(n-1) + fib(n-2). In the if line the condition should include cases n = 1 and n = 2, which return Fib(n)=1. Therefore, the line begins with if(n==1 || n==2) ... In the next line, the term n*Factori(n-1) is replaced by the second member of the formula of Fib(n) above. A suggestion for the argument of the last printf() is "\n Fib (%d)=%6d", i, k `. The third proposed amendment is the introduction of a for before the ‘k =’ with a variable j (include it in the declaration) ranging from 1 to i, so that all values of the sequence, until it reaches the ith, are printed. In calling the Fib(), the argument should obviously be the variable j. And the argument of the printf() should be something like "%6d", k’.

# Fast sorting

The Quicksort algorithm was developed by C. A. R. Hoare and published in 1962 (Computer Journal, paragraph 5, pp. 10-15). It is, today, the fastest method of ordering, numeric or alphanumeric, and has recursion on its strong point.

In C it looks like this:

Example-program #12B