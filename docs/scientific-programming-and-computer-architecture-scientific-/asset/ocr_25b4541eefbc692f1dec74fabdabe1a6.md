# 4.2. Optimizing memory access

265

```
scratch);
}
```

This function implicitly partitions $A$ into $3000 	imes 200$ blocks, $B$ into $200 	imes 3000$ blocks, and $C$ into $3000 	imes 3000$ blocks. The function `mult_3000x200x3000()`, defined at the previous stage, is used to multiply a single block of $A$ into a single block of $B$ to get a single block of $C$.

The floating point bandwidth realized is 3.19 flops per cycle for the multiplication of square matrices of dimension 9000 on a 2.6 GHz SSE2 machine. For the same problem, the MKL library realizes more than 3.8 flops per cycle. Why is our design worse? The bulk of blame falls on the microkernel. To begin, the microkernel yields only 3.48 flops per cycle, assuming all its arguments are in L1 cache. On a 3.6 GHz AVX2 machine, which the microkernel yields 3.98 flops per cycle, the bandwidth realized for the multiplication of square matrices is 3.75 flops per cycle.

**Exercise 4.2.1.** The function sum() of section 4.2 adds an array of numbers in sequence. Assuming the array to be several gigabytes long, explain why the number of cycles consumed by the function depends solely on memory access, with the additions not any extra overhead.

**Exercise 4.2.2.** Initialize a long array. Sum its entries with a stride that ensures only one entry is read from a page. What is the peak bandwidth to memory realized? That is the peak bandwidth to DRAM in the presence of TLB misses.

**Exercise 4.2.3.** Write a program to measure the bandwidth of writing to DRAM memory. Compare write bandwidth to read and copy bandwidth given in table 4.4.

**Exercise 4.2.4.** Explain why the bandwidth in table 4.4 is lower than the read bandwidth.

**Exercise 4.2.5.** Write a program that maps an $n 	imes n$ array of numbers to another $n 	imes n$ array, with each entry replaced by the average of north, south, east, and west entries. The arrays are assumed to be in column-major order. Compare the speed of a program that traverses the arrays columnwise with a program that traverses the arrays rowwise. Why do you expect columnwise traversal to be faster? Implement the computation using blocking. Explain why blocking is likely to make the program faster.