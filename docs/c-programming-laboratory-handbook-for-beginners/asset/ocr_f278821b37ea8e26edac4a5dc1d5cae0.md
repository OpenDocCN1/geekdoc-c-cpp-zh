# ### *omp_get_thread_num Function*

The omp_get_thread_num function returns the thread number, within its team, of the thread executing the function. The thread number lies between 0 and omp_get_num_threads()–1, inclusive. The master thread of the team is thread 0.

The format is as follows:

```
```cpp
#include <omp.h>
int omp_get_thread_num(void);
```
```

If called from a serial region, omp_get_thread_num returns 0. If called from within a nested parallel region that is serialized, this function returns 0.

# ## Theory

# ### *Parallel Computing*

+   - Traditionally, software has been written for serial computation.
+   - Parallel computing is the simultaneous use of multiple compute resources to solve a computational problem.
+   - In this technique a large problem can be divided into smaller segments which can be solved independently and simultaneously; the computers that facilitate parallel coding are called parallel computers.

# ### *Prime Numbers*

+   - A prime number (such as 2 or 3 or 5) is a natural number (positive whole number) which is only divisible by itself and by 1 (and no other natural number).
+   - The prime numbers less than 100 are:
+   
+     2 3 5 7 11 13 17 19 23 29 31 37 41 43 47 53 59 61 67 71 73 79 83 89 97.

# ### *Sieve of Eratosthenes Algorithm*

This process is called the Sieve of Eratosthenes, after the Greek mathematician, from Alexandria, who invented it. He is also the man who first measured the circumference of the earth. This method, of listing primes, is called a “sieve” because it is like taking all of the numbers (up to some maximum) and running them through a sieve to separate out all of the primes.

# ### *Sieve of Eratosthenes Method*

+   - There is a fairly simple method for making a list of primes. We will start with a list of all of the numbers from 2 to 100:
+   
+     0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34
+     35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65
+     66 67 68 69 70 71 72 73 74 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 91 92 93 94 95 96
+     97 98 99 100
+   - We now make 2 bold (you can circle it), identifying it as prime (it is not divisible by lesser primes), and cross out every second number after 2: