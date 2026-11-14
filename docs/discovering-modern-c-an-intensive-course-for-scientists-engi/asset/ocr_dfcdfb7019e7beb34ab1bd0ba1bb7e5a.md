```
data[i] = that[i];
return *this;
};
```

This assignment operator accepts every type except vector<-t> for which we need a dedicated copy-assignment operator. To avoid code redundancy, we could implement a method that performs the actual copy and is called from both the general and the copy assignment.

# Advantages of expression templates:

Although the availability of operator overloading in C++ resulted in notationally nicer code, the scientific community refused to give up programming in Fortran or to implement the loops directly in C/C++. The reason was that the traditional operator implementations were too expensive. Due to the overhead of creating temporary variables and of copying vector and matrix objects, C++ could not compete with the performance of programs written in Fortran. This problem has been resolved with the introduction of generics and expression templates. Now we can write extremely efficient scientific programs in a notationally convenient manner.

# 5.4 Meta-Tuning: Write Your Own Compiler Optimization

Compiler technology is progressing, and more and more optimization techniques are provided. Ideally, we all write software in the easiest and most readable way, and the compiler generates the optimal executable out of it. We would only need a newer and better compiler for our programs to become faster and faster. Unfortunately, this only sometimes really works.

In addition to general-purpose optimizations like copy elision (§2.3.5.3), compilers provide numeric optimization techniques like Loop Unrolling: the loop is transformed such that multiple iterations are performed in one. This decreases the overhead of loop control and increases the potential for concurrent execution. Many compilers apply this technique only on the inner loop whereas unrolling multiple loops often enables even better performance. Several iterative calculations benefit from the introduction of additional temporaries which in turn can require semantic information that is not available for user types or operations.

Some compilers are particularly tuned for specific operations—especially those used in benchmarks and even more specifically for the LINPACK benchmark used to rate the 500 fastest computers in the world (www.top500.org). For instance, they can use pattern matching to recognize the typical three-nested loop in canonical dense-matrix multiplication and replace this code with a highly tuned assembler implementation that can be one or more orders of magnitude faster. These programs use seven or nine loops with platform-dependent block size to squeeze out the last bit of every cache level, transpose sub-matrices, run on multiple threads, perform a filigree register choreography, and so on.5

5. One could sometimes get the impression that the High-Performance Computing (HPC) community believes that multiplying dense matrices at near-peak performance solves all issues of the world or at least demonstrates that everything can be computed at near-peak performance if only one tries hard enough. Enviously, more and more people in the supercomputer centers realize that their machines are not only running dense matrix operations and that real-world applications are in most cases limited by memory bandwidth and latency.