# **Example 9.6:**

As the relationship t4 = 4 * j surely holds after assignment to t4 in Fig. 9.5, and t4 is not changed elsewhere in the inner loop around B₂, it follows that just after the statement j = j−1 the relationship t4 = 4 * j + 4 must hold. We may therefore replace the assignment t4 = 4*j by t4 = t4−4. The only problem is that t4 does not have a value when we enter block B₃ for the first time.

Since we must maintain the relationship t4 = 4 * j on entry to the block B₃, we place an initialization of t4 at the end of the block where itself is initialized, shown by the dashed addition to block B₁ in Fig. 9.8. Although we have added one more instruction, which is executed once in block B₁, the replacement of a multiplication by a subtraction will speed up the object code if multiplication takes more time than addition or subtraction, as is the case on many machines.

![](bbox=[0.262, 0.393, 0.738, 0.799])

Figure 9.9: Flow graph after induction-variable elimination

We conclude this section with one more instance of induction-variable elim-