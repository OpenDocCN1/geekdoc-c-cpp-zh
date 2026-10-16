In Figure 13.4 the four procedures m_set_procs, m_fork, m_kill_procs, and m_get_myid are imported from a library (the parallel/parallel library). m_set_procs and m_kill_procs are as in the previous example. m_fork creates the 10 processes, which are all instances of the procedure multiply (the name fork comes from the UNIX operating system, discussed shortly). In procedure multiply, m_get_myid gets the number of the process instance (from 0 to 9). The remainder of the code then divides the work among the processes, so that process 0 calculates c[0][i], c[10][i], …, c[90][i] for all i, process 2 calculates c[2][i], c[12][i], …, c[92][i], and so on.

A final alternative to introducing parallelism into a language is to simply rely on operating system features directly to run programs in parallel. Essentially, this requires that a parallel program be split up into separate, independently executable pieces and then set up to communicate via operating system mechanisms (thus, allowing only program-level parallelism as described shortly). A typical example of this is to string programs together in a UNIX operating system through the use of pipes, which is a method of streaming text input and output from one program to another without storing to intermediate files (which could be inefficient or impossible if these files are large). A simple example is the following, which will list all filenames in the current directory containing the string "java":

```
ls | grep "java"
```

This command runs the two UNIX utility programs ls and grep in parallel (ls is the directory listing program; grep is the "global regular expression print" program that finds string patterns in text). The output of ls is piped to grep using the pipe symbol (the vertical bar), and becomes the input to grep. As a more complex example, the pipe

```
cat *_java | tr -sc A-Za-z `\012` | sort | uniq -c | sort -rn
```

will list all of the words in Java programs in the current directory, with a count of their usage, and sorted in order of decreasing number of uses (we leave as an exercise for the reader the explanation of each of the five programs used in this pipeline).

# 13.2.2 Process Creation and Destruction

A programming language that contains explicit mechanisms for parallel processing must have a construct for creating new processes. You have seen this informally already in Figure 13.4, where calls to the library procedures m_set_procs and m_fork together created a fixed number of processes.

There are two basic ways that new processes can be created. One is to split the current process into two or more processes that continue to execute copies of the same program. In this case, one of the processes is usually distinguished as the parent, while the others become the children. The processes can execute different code by a test of process identifiers or some other condition, but the basic program is the same for all processes. This method of process creation resembles the SIMD organization of Section 13.1 and is, therefore, called SPMD programming (for single program multiple data). Note, however, that SPMD programs may execute different segments of their common code and so do not necessarily operate synchronously. Thus, there is a need for process synchronization.

> *This can actually be condensed to the single command "ls *java*" in UNIX.