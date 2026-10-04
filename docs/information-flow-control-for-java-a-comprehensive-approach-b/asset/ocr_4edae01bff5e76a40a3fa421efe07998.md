# CHAPTER 3. CONCURRENCY

cept FacThreads.run the algorithm will branch to $\theta(n) \= method(\theta(c))$, they will be assigned thread number 0, which eventually reaches a fixed point. FacThreads.run is forked from a callsite FacThreads, a definition of Thread. Therefore the first branch is executed which determines that there be several threads spawned from callsite, as a consequence of being invoked in a loop. Thus, FacThreads.run is assigned two virtual threads, 1 and 2.

We use virtual threads as an approximation of $\theta$ when computing interference dependence. Thus, when thread primes interference dependence for the second requirement of Definition 3.1.

# 3.3 Dependence Analysis for Concurrent Programs

Thread numbers give an initial approximation with which threads execute in parallel. With these numbers, we use the spirit of Sprite [Kri98 Kri03b] who assumes all threads executing concurrently from the start to the program's termination. But in contrast to previous works, we generalize to dynamic thread creation instead of working with a statically fixed set of 'tasks'

# 3.3.1 Interference Dependence

One requirement of analyzing threaded software is to find possible dependences due to data being changed by a concurrently executing thread as presented in Definition 3.1. However, this definition needs to refine to Java's memory model:

> Definition 3.2. A node $r$ is interference dependent on node $d$, if $\theta(d) \neq \thetatheta(r)$ ($d$ and $r$ may potentially be executed in parallel)

+   1. either there is a static field $f$, such that $d$ defines $f$ and $r$ references $f$,n2. or there is a (non-static) field $f$, such that $d$ defines $f$ of value $v$ and $r$ references $f$ of variable $w$, and $v$ and $w$ are potential aliases.

While this analysis is still imprecise compared to the Java memory model as presented, it improves significantly over previous works, which did not introduce interference analysis on aliasing of variable bases, but by using [Zha99,HCD99] (i.e. all reads of a given field $f$ are interference dependence on all writes to $f$, ignoring the base variables) or escape analysis [RH04] (access to a given field $f$ of object $o$ have interference if $o$ is found to be escaping the thread.)

Definition 3.2 gives rise to Algorithm 3.4
Coming back to the table of Figure 3.5, with the virtual thread numbers in the methods with 0 and FacThreads.run can only find interference between the methods and run from the latter to itself.
However, FacThreads.run does not contain definitions of shared variables, so

> "Ranganath was a highly efficient but Admittedly imprecise unification based escape analysis by Ruf's approach [Ruf00].