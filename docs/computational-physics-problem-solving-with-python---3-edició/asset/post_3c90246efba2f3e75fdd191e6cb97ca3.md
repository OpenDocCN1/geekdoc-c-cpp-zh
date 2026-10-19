
Rule 4 Remember the 80/20 rule: In many fields you can get 80% of the result with 20% of the effort (also called the 90/10 rule – it depends on who you talk to). Whenever you're about to optimize code, use profiling to find out where that 80% of execution time is going, so you know where to concentrate your effort.

Rule 5 Always run “before” and “after” benchmarks: How else will you know that your optimizations actually made a difference? If your optimized code turns out to be only slightly faster or smaller than the original version, undo your changes and go back to the original, clear code.

Rule 6 Use the right algorithms and data structures: Do not use an O(n²) DFT algorithm to do a Fourier transform of a 1000 elements when there is an O(n log n) FFT available. Similarly, do not store a thousand items in an array that requires an O(n) search when you could use an O(log n) binary tree or an O(1) hash table (Hardwich, 1996).

The type of optimization often associated with high-performance or numerically intensive computing is one in which sections of a program are rewritten and reorganized in order to increase the program's speed. The overall value of doing this, especially as computers have become so fast and so available, is often a subject of controversy between computer scientists and computational scientists. Both camps agree that using the optimization options of compilers is a good idea. Yet on the one hand, CS tends to think that optimization is best left to the compilers, while computational scientists, who tend to run large codes with large amounts of data in order to solve real-world problems, often believe that you cannot rely on the compiler to do all the optimization.

## 11.1.1
### Programming for Virtual Memory (Method)

While memory paging makes little appear big, you pay a price because your program's run time increases with each page fault. If your program does not fit into RAM all at once, it will be slowed down significantly. If virtual memory is shared among multiple programs that run simultaneously, they all cannot have the entire RAM at once, and so there will be memory access conflicts which will decrease performance. The basic rules for programming for virtual memory are:

- 1. Do not waste your time worrying about reducing the amount of memory used (the working set size) unless your program is large. In that case, take a global view of your entire program and optimize those parts that contain the largest arrays.
- 2. Avoid page faults by organizing your programs to successively perform their calculations on subsets of data, each fitting completely into RAM.
- 3. Avoid simultaneous calculations in the same program to avoid competition for memory and consequent page faults. Complete each major calculation before starting another.
- 4. Group data elements close together in memory blocks if they are going to be used together in calculations.

## 11.1.2
### Optimization Exercises

Many of the optimization techniques developed for Fortran and C are also relevant for Python applications. Yet while Python is a good language for scientific programming and is as universal and portable as Java, at present Python code runs slower than Fortran, C or even Java codes. In part, this is a consequence of the Fortran and C compilers having been around longer and thereby having been better refined to get the most out of a computer's hardware, and in part this is also a consequence of Python not being designed for speed. Because modern computers are so fast, whether a program takes 1s or 3s usually does not matter much, especially in comparison to the hours or days of your time that it might take to modify a program for increased speed. However, you may want to convert the code to C (whose command structure is similar to that of Python) if you are running a computation that takes hours or days to complete and will be doing it many times.

Especially when asked to, compilers may look at your entire code as a single entity and rewrite it in an attempt to make it run faster. In particular, Fortran and C compilers often speed up programs by being careful in how they load arrays into memory. They also are careful in keeping the cache lines full so as not to keep the CPU waiting or having it move on to some other chore. That being said, in our experience compilers still cannot optimize a program as well as can a skilled and careful programmer who understands the order and structure of the code.

There is no fundamental reason why a program written in Java or Python cannot be compiled to produce a highly efficient code, and indeed such compilers are being developed and becoming available. However, such code is optimized for a particular computer architecture and so is not portable. In contrast, the byte code (.class file in Java and .pyc file in Python) produced by the compiler is designed to be interpreted or recompiled by the Java or Python Virtual Machine (just another program). When you change from Unix to Windows, for example, the Virtual Machine program changes, but the byte code is the same. This is the essence of portability.

In order to improve the performance of Java and Python, many computers and browsers run Just-in-Time (JIT) compilers. If a JIT is present, the Virtual Machine feeds your byte code Prog.class or Prog.pyc to the JIT so that it can be recompiled into native code explicitly tailored to the machine you are using. Although there is an extra step involved here, the total time it takes to run your program is usually 10–30 times faster with a JIT as compared to line-by-line interpretation. Because the JIT is an integral part of the Virtual Machine on each operating system, this usually happens automatically.

In the experiments below, you will investigate techniques to optimize both Fortran and Java or Python programs, and to compare the speeds of both languages for the same computation. If you run your program on a variety of machines you should also be able to compare the speed of one computer to that of another. Note that a knowledge of Fortran or C is not required for these exercises; if you keep an open mind you should be able to look at the code and figure out what changes may be needed.

### 11.1.2.1 Good and Bad Virtual Memory Use (Experiment)

To see the effect of using virtual memory, convert these simple pseudocode examples (Listings 11.1 and 11.2) into actual code in your favorite language, and then run them on your computer. Use a command such as time, time.clock() or timeit to measure the time used for each example. These examples call functions force12 and force21. You should write these functions and make them have significant memory requirements.

# Listing 11.1 BAD program, too simultaneous.

```
for j = 1, n; { for i = 1, n; {
  f12(i,j) = force12(pion(i), pion(j))    // Fill f12
  f21(i,j) = force21(pion(i), pion(j))    // Fill f21
  ftot = f12(i,j) + f21(i,j) }}          // Fill ftot
```

You see (Listing 11.1) that each iteration of the for loop requires the data and code for all the functions as well as access to all the elements of the matrices and arrays. The working set size of this calculation is the sum of the sizes of the arrays f12(N,N), f21(N,N), and pion(N) plus the sums of the sizes of the functions force12 and force21.

A better way to perform the same calculation is to break it into separate components (Listing 11.2):

# Listing 11.2 GOOD program, separate loops.

```
for j = 1, n;
  { for i = 1, n;  f12(i,j) = force12(pion(i), pion(j)) }
for j = 1, n;
  { for i = 1, n;  f21(i,j) = force21(pion(i), pion(j)) }
for j = 1, n;
  { for i = 1, n;  ftot = f12(i,j) + f21(i,j) }
```

Here, the separate calculations are independent and the working set size, that is, the amount of memory used, is reduced. However, you do pay the additional overhead costs associated with creating extra for loops. Because the working set size of the first for loop is the sum of the sizes of the arrays f12(N, N) and pion(N), and of the function force12, we have approximately half the previous size. The size of the last for loop is the sum of the sizes for the two arrays. The working set size of the entire program is larger than of the working set sizes for the different for loops.

As an example of the need to group data elements close together in memory or common blocks if they are going to be used together in calculations, consider the following code (Listing 11.3):
