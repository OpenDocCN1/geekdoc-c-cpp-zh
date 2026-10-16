
## 13.28 The Java semaphore code in Figure 13.7 is overly simple, because of the possibility of interrupts. Here is an improved version for the delay() procedure:

```
// adapted from Lea [2000], p. 267

public void delay() throws InterruptedException{
    if (Thread.interrupted())
        throw new InterruptedException();
    synchronized(this){
        try{
            while (count <= 0) wait();
            count--;
        }catch(InterruptedException ie){
            notify(); throw ie;
        }
    }
}
```

Explain carefully the reason for each of the differences between this code and the code of Figure 13.7.

## 13.29 Explain the behavior of the Java code for the bounded buffer problem if the keyword synchronized is removed from the put operation (line 28 of Figure 13.6).

## 13.30 In Ada, you saw that the bounded buffer could be represented either by task or a monitor. Is one of these solutions preferred over the other? Why?

## 13.31 A shared-memory system can imitate the mailbox version of message passing by defining a mailbox utility using mutual exclusion. Write a package to implement mailboxes (i.e., queues of data with send and receive primitives) in:
(a) Java
(b) Ada

## 13.32 In Ada, the caller of an entry must suspend execution during the execution of the corresponding accept-statement. Why is this necessary?

## 13.33 In an Ada select alternative, an accept-statement can be followed by more statements. For example, in the bounded buffer solution in Ada, we wrote:

```
accept insert (ch: in character) do
    bufferEnd := bufferEnd mod MaxBufferSize + 1;
    store (bufferEnd) := ch;
end insert;
bufferSize := bufferSize + 1;
```

Note that bufferSize is incremented outside the accept statement. Is there a reason for this? Could the statement be put inside the accept? Could the statement store(bufferEnd) := ch be moved out of the accept? Why?

```
task body Mult is
    begin
        accept DoRow (i: in INTEGER ) do
            for j in 1..Size loop
                c(i, j) := 0;
                for k in 1..Size loop
                    c(i, j) := c(i, j) + a(i, k)*b(k, j);
                end loop;
            end loop;
        end;
    end Mult;
```

What is wrong with this solution?

## 13.41 This chapter ignored the question of formal semantics for concurrent programs. (Some studies are mentioned in the references.) Can you think of problems that may be encountered in applying axiomatic semantics to concurrent programs? What about denotational semantics?

## 13.42 The matrix multiplication solution in Ada of Figure 13.13 uses the size of the matrix to determine the number of tasks. Rewrite the solution to use a number of tasks specified as an input parameter to the ParMult function.

## 13.43 Or-parallelism in Prolog can be viewed as a parallel search of the tree of alternatives (see Chapter 4), where at each node a new process is created to search each child. Describe how these processes can coordinate their activities to allow backtracking.

## 13.44 Write a procedure to perform a parallel search of an unordered binary tree in:
(a) Java
(b) Ada

## 13.45 Discuss the claim made in the text that or-parallelism is more natural for Prolog, whereas and-parallelism is more natural for Lisp.

## 13.46 Describe in detail the way or-parallel Prolog computes the three solutions to delete([1,2,3],X,T) in parallel. What time savings would you expect (in terms of numbers of steps)?

## 13.47 How much actual parallelism is performed in the and-parallel Prolog example of generate on page 625? Explain.

## 13.48 In and-parallel Prolog, if a guard encounters an uninstantiated variable, execution is suspended until the variable is instantiated (by another process). Why is this necessary? Are there any problems with this requirement?

## 13.49 Explain why backtracking is difficult in and-parallel Prolog.

## 13.50 In Figures 13.4 and 13.5, the main process creates new child processes to compute the matrix product and then suspends until all the child processes have finished. This is wasteful. Rewrite these programs so that the main process also performs some computations in parallel with its children.

## 13.51 Compare the notion of mailbox to that of a buffer.

## 13.52

Suppose that two processes both attempt to increment a shared variable S that is unprotected by a mutual exclusion mechanism. Suppose the assignment

S := S + 1

consists within each process of three machine instructions:

+   Load S into a reg
+   Increment the reg
+   Store the reg to S

What values might S have after both processes complete their increment operations? Show how each value can be obtained.

## Notes and References

The field of parallel/concurrent programming is a huge one, involving operating system, architecture, and language issues. In this chapter, we have barely touched on specific language issues, using primarily Java and Ada as our examples. Typically, an entire course is devoted to parallel programming, often using one of the language-independent protocols supported by third-party libraries. Two examples of useful texts in this area are Andrews [2000] and Wilkinson and Allen [1997].

Surveys of parallel programming languages include the September 1989 issue of ACM Computing Surveys (Vol. 21, No. 3) and the July 1989 issue of IEEE Software. Some individual articles from these issues are also mentioned in the following. Another survey article is Andrews and Schneider [1983].

Programming using Java threads is studied in Lea [2000], Horstmann and Cornell [1999] (Vol. II), and Arnold et al. [2000]. For an alternative view of threads, see Butenhof [1997], which describes the Pthreads standard for UNIX. Programming using Ada tasks and Ada95 protected types is studied in Cohen [1996]; see also Wegner and Smolka [1983].

A survey of parallel architectures appears in Duncan [1990]. The diagrams in Section 13.1 are adapted from Karp [1987], where several methods of adding parallelism to FORTRAN are also studied. See also Karp and Babb [1988] for examples similar to those of Section 13.2.

Semaphores were introduced by Dijkstra [1968b]. See Stallings [2000] for a study of their use in operating systems. Monitors were introduced by Hoare [1974] and made part of the Concurrent Pascal language designed by Brinch-Hansen [1975].

The question of scheduling policies, fairness, and starvation were only mentioned briefly in this chapter, and the associated issue of process priorities was not discussed at all. For a discussion of the Java approach, see Lea [2000], especially Sections 3.4.1 and 3.7. For a discussion of the Ada95 approach, see Cohen [1996], Section 18.6.

Message passing, including a theoretical framework called Communicating Sequential Processes, or CSP, was introduced by Hoare [1978]. CSP is often used as a basis for formal semantics and verification of concurrent programs; see Schneider [2000]. CSP was also the inspiration for the programming language Occam, designed to run on a proprietary parallel system called the transputer; see Jones and Goldsmith [1988]. For a different approach to formal semantics of concurrent programs using a technique called process algebra, see Milner [1994].

A description of Multilisp is in Halstead [1985]. QLisp is described in Goldman and Gabriel [1989]. Surveys of parallel logic programming include Kergommeaux and Codognet [1994], Ciancarini [1992], Shapiro [1989], and Tick [1991]. Parlog is studied in Conlon [1989], Gregory [1987], and Ringwood [1988]. FGHC is described in Ueda [1987]. Concurrency and constraints in logic programming (Chapter 4) are closely related; see Ueda [2000] or Saraswat and Van Hentenryck [1995].

Information on various protocols for distributed parallel computing on networks can be found in Horstmann and Cornell [1999], Vol. II (Java’s RMI), and Pacheco [1996] (MPI). Books on CORBA and COM are too numerous to mention, since these protocols are used for program interoperability as well as concurrency. A brief introduction can be found in Horstmann and Cornell [1999].

Several projects have used the Internet as a large parallel processing system; perhaps the best known is the Great Internet Mersenne Prime Search Project (see www.mersenne.org), which currently holds the record for the largest known prime number.

Erlang is described in Armstrong [2007] and [2010].
