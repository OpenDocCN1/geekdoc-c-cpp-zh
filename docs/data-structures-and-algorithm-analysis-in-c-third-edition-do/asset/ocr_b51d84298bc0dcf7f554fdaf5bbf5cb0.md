# 17.4 Further Reading

a function as part of a program) to take $P$ and some input string $w$, and modify it so that $w$ is hardcoded inside $P'$, with $P$ reading no input. Call this modified program $P'$. $P'$ always behaves the same regardless of its input, it ignores all input. However, because $w$ is now hardwired inside of $P'$, the behavior we get is that of $P$ when $w$ as input. So, $P'$ will halt on any arbitrary input if and only if $P$ would halt on input $w$. We need $P'$ to halt $Ahalt$. If $Ahalt$ could determine $P'$ halts on some input, then that is the same as determining that $P$ halts on input $w$. But we know that that is impossible. Therefore, $Ahalt$ cannot exist.

There are many things that we would like to have a computer do are unsolvable. Many of these have to do with program behavior. For example, proving that an arbitrary program is "correct," proving that a program computes a particular function, is a proof reading program behavior. As such, what can be achieved is limited. Other unsolvable problems include:

+   * Does a program halt on every input?
* Does a program compute a particular function?
* Do two programs compute the same function?
* Does a particular line in a program executed?

This does not mean that a computer program cannot be written that works on special cases, possibly even on most programs that we would be interested in checking. For example, if $C$ compilers will check if the control expression for a **while** loop is a constant expression that evaluates to false. If it is, the compiler will issue a warning that the **while** loop code will never be executed. However it is not possible to write a computer program that can check for all input whether a specific line of code will be executed when the program is given some input.

Another unsolvable problem is whether a program contains a computer virus. The property "computer virus" is a matter of behavior. Thus, it is not possible to determine positively whether an arbitrary program contains a computer virus. Frankly, there are many good heuristics for determining if a program is likely to contain a virus, and it is usually possible to determine if a program contains a particular virus, at least the ones that are now known. It will always be possible for malicious people to invent new viruses that no virus checker can recognize.

# 17.4 Further Reading

The classic text on the theory of $NP$-completeness is *Computers and Intractability: A Guide to the Theory of NP-completeness* by Garey and Johnston [GJ79]. The Traveling Salesman Problem*, edited by Lawler et al. [LLKS85], discusses