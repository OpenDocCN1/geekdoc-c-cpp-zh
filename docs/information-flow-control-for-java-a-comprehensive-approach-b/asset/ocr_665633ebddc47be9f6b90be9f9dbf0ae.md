# 3.2. SLICING CONCURRENT JAVA

```
int x,y;

main() {
  x = 0;
  y = 1;
  fork(thread_1);
  int p = x - 2;
  int q = p + 1;
  y = q + 3;
}

thread_1() {
  int a = y + 1;
  int b = a + 4;
  x = b / 2;
}
```

![](bbox=[0.315, 0.143, 0.823, 0.313])

Figure 3.1: An example cSDG

# 3.2.1 Undecidability of Slicing

Precise slicing is undecidable in general. Several undecidability results have impact on the slicing technique for concurrent programs:

+   1. Whether a condition becomes true or false in the run of a program cannot be statically decided. To circumvent this, one generally assumes non-deterministic choice at conditionals during static analysis, the consequence that every path in the interprocedural CFG is assumed to be feasible (see chapter 2, page 23).

+   2. Precise slicing of languages with respect to synchronization and recursion is undecidable [Ram00].

+   3. In combination with interference dependence, data dependence is no longer transitive [MOS01], rendering parallel interprocedural slicing undecidable altogether.

In the following, we will present another source of undecidability: Precise interprocedural slicing [Kri98] in combination with dynamic thread creation is undecidable.

To illustrate the results (2) and (3), consider Figure 3.2, which shows small example programs. The program on the left demonstrates how synchronization can induce an order on the execution sequence: first a is set to 1, after the other thread can proceed and will kill the first definition assigning to 0. So the difference between a:=1 and write(a) could be removed.

In the example right (taken from [MOS01]), the value of write(c) will not have influence on any possible execution sequence. The statement in the right might either be scheduled before b:=0 or after. If it executes, then c will be redefined in the first thread before the join. If not, b will already be redefined to 0, and thus independent from the value of a.

The works cited above show that the effects presented in these examples