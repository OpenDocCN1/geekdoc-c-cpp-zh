2.15 Give an efficient algorithm to determine if there exists an integer $i$ such that $A_i = i$ in an array of integers $A_1 < A_2 < A_3 < \cdots < A_n$. What is the running time of your algorithm?

2.16 Write an alternative gcd algorithm based on the following observations (arrange so that $a > b$):
a. $gcd(a, b) = 2gcd(a/2, b/2)$ if $a$ and $b$ are both even.
b. $gcd(a, b) = gcd(a/2, b)$ if $a$ is even and $b$ is odd.
c. $gcd(a, b) = gcd(a, b/2)$ if $a$ is odd and $b$ is even.
d. $gcd(a, b) = gcd((a + b)/2, (a - b)/2)$ if $a$ and $b$ are both odd.

* 2.17 Give efficient algorithms (along with running time analyses) to
\* a. Find the minimum subsequence sum.
\* b. Find the minimum positive subsequence sum.
\* c. Find the maximum subsequence product.

2.18 An important problem in numerical analysis is to find a solution to the equation $f(x) = 0$ for some arbitrary $f$. If the function is continuous and has two points $low$ and $high$ such that $f(low)$ and $f(high)$ have opposite signs, then a root must exist between $low$ and $high$ and can be found by a binary search. Write a function that takes as parameters $f$, $low$, and $high$ and solves for a zero. What must you do to ensure termination?

2.19 The maximum contiguous subsequence sum algorithms in the text do not give any indication of the actual sequence. Modify them so that they return in a single object the value of the maximum subsequence and the indices of the actual sequence.

2.20 a. Write a program to determine if a positive integer, $N$, is prime.
b. In terms of $N$, what is the worst-case running time of your program? (You should be able to do this in $O(\sqrt{N})$.)
c. Let $B$ equal the number of bits in the binary representation of $N$. What is the value of $B$?
d. In terms of $B$, what is the worst-case running time of your program?
e. Compare the running times to determine if a 20-bit number and a 40-bit number are prime.
f. Is it more reasonable to give the running time in terms of $N$ or $B$? Why?

* 2.21 The Sieve of Eratosthenes is a method used to compute all primes less than $N$. We begin by making a table of integers 2 to $N$. We find the smallest integer, $i$, that is not crossed out, print $i$, and cross out $i, 2i, \dots$. When $i > \sqrt{N}$, the algorithm terminates. What is the running time of this algorithm?

2.22 Show that $x^{62}$ can be computed with only eight multiplications.

2.23 Write the fast exponentiation routine without recursion.

2.24 Give a precise count on the number of multiplications used by the fast exponentiation routine. (Hint: Consider the binary representation of $N$.)

2.25 Programs $A$ and $B$ are analyzed and found to have worst-case running times no greater than $150N \log_2 N$ and $N^2$, respectively. Answer the following questions, if possible: