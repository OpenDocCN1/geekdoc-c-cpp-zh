# 13.7.2 Or-Parallelism

In or-parallelism, execution of several alternatives can occur in parallel, with the first alternative to finish (or succeed) causing all other alternative processes to be ignored (and to terminate). In Lisp, an example of such parallelism can occur in the evaluation of a cond expression:

```
(cond (p1 e1) (p2 e2) ... (pn en))
```

In this situation, it may be possible for the e_i that correspond to true p_i conditions to be evaluated in parallel, with the first value to be computed becoming the value of the cond expression. (It may also be possible to compute the p_i themselves in parallel.) In this case, it may also be necessary to synchronize the computations. However, there is another problem as well: or-parallel computation makes the cond into a nondeterministic construct (similar to Dijkstra’s guarded if), which may change the overall behavior of the program if the order of evaluation is significant. For example, an else-part in a cond should not be evaluated in parallel with the other cases.

In Prolog, or-parallelism is also possible in that a system may try to satisfy alternative clauses for a goal simultaneously. For example, if there are two or more clauses for the same predicate,

```
p(X) :- q(X).
p(X) :- r(X).
```

a system may try to satisfy q and r in parallel, with p succeeding with X instantiated according to the one that finishes first (or perhaps even saving other instantiations in a queue). In fact, this is consistent with the semantics of pure logic programming, since alternative goals are satisfied nondeterministically. However, in common Prolog implementations, the correct execution of a program may depend on the order in which alternatives are tried. In this case, a strict ordering may need to be applied. For example, in a common program for factorial in Prolog,

```
fact (X, Y) :- X = 0 , ! , Y = 1.
fact (X, Y) :- Z is X - 1, fact (Z, Y1), Y is X * Y1.
```

the first clause needs to be tried before the second (or reaching the cut in the first should terminate the second).

The synchronization and order problems we have mentioned for both and-parallelism and or-parallelism are difficult to solve automatically by a translator. For this reason, language designers have experimented with the inclusion of a number of manual parallel constructs in non-imperative languages. In some cases, these are traditional constructs like semaphores or mailboxes, with modified semantics to provide better integration into the language. In other cases, more language-specific means are used to indicate explicit parallelism.

There is, however, another argument for the inclusion of explicit parallelism in non-imperative languages. In many situations, one may wish to suppress the creation of small (i.e., fine-grained) processes when the computational overhead to create the process is greater than the advantage of computing the result in parallel. This may be the case, for example, in highly recursive processes, where as one approaches the base case, one may not want to create new processes but switch to ordinary computation. Or, one may wish to suppress parallel computation altogether when the values to be computed have a small computational overhead.

Next, we examine a few of the explicit parallel mechanisms employed in some of the parallel Lisps and Prologs mentioned earlier in this chapter.