# Lemma

Under the current naming conventions, $A_b^{(m)}$ is complete, and $A_b^{(m-1)}$ is almost complete. Furthermore, the missing number in $A_b^{(m-1)}$ is obtained from the missing number in $A_b^{(m)}$ by removing the least significant bit (i.e., shift right).

# Proof

First we will see an example and then make a formal proof. To use the previously given example with $n=10$, $m=4$, missing number $6=0110_b$, and $A$ as

![](bbox=[0.286, 0.293, 0.756, 0.407])

the two derived subarrays: $A_0^{(3)}$ and $A_1^{(3)}$ are respectively:

![](bbox=[0.399, 0.468, 0.643, 0.556])

![](bbox=[0.401, 0.581, 0.642, 0.656])

Obviously, $A_0^{(3)}$ is almost complete and $A_1^{(3)}$ is complete: column $\{0\ 1\}$ is missing from it. The last significant bit of the missing number in $A$ is 0; if we did not know which is the missing number, we could deduce that its least significant bit is 0 by computing the aforementioned $\Delta=5-5=0$. Indeed, $A_0^{(3)}=A^{(3)}$ is the array that is almost complete. And indeed the missing number in it $0110_b$ is obtained from $0110_b$ by shift right.

Let us prove it. It is clear that if $A$ is a complete array of size $n$, both $A_0^{(m-1)}$ and $A_1^{(m-1)}$ are not complete. If $n$ is odd then they contain the same columns (possibly in different order left to right), otherwise $A_1^{(m-1)}$ contains one column more and the other columns are the same.