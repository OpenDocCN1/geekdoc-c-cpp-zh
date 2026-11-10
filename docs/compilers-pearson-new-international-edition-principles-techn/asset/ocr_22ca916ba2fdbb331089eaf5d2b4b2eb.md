# 10.4. GLOBAL CODE SCHEDULING

**Exercise 10.3.3:** Repeat Exercise 10.3.2 assuming:

+   i. The machine has one ALU resource and two MEM resources.
+   
+   ii. The machine has two ALU resources and one MEM resource.
+   
+   iii. The machine has two ALU resources and two MEM resources.

```
1)  LD R1, a
2)  ST b, R1
3)  LD R2, c
4)  ST c, R1
5)  LD R1, d
6)  ST d, R2
7)  ST a, R1
```

Figure 10.11: Machine code for Exercise 10.3.4

**Exercise 10.3.4:** Assuming the machine model of Example 10.6 (as in Exercise 10.3.2):

+   a) Draw the data dependence graph for the code of Fig. 10.11.
+   
+   b) What are all the critical paths in your graph from part (a)?
+   
+   c) Assuming unlimited MEM resources, what are all the possible schedules for the seven instructions?

# 10.4  Global Code Scheduling

For a machine with a moderate amount of instruction-level parallelism, schedules created by compacting individual basic blocks tend to leave many resources idle. In order to make better use of machine resources, it is necessary to consider code-generation strategies that move instructions from one basic block to another. Strategies that consider more than one basic block at a time are referred to as *global scheduling* algorithms. To do global scheduling correctly, we must consider not only data dependences but also control dependences. We must ensure that

+   1. All instructions in the original program are executed in the optimized program, and
+   
+   2. While the optimized program may execute extra instructions speculatively, these instructions must not have any unwanted side effects.