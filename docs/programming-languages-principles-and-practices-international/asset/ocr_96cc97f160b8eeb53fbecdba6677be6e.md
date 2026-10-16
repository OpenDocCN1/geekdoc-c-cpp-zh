In the second method of process creation, a segment of code (commonly a procedure) is explicitly associated with each new process. Thus, different processes have different code, and we can call this method **MPMD programming**. A typical case of this is the so-called **fork-join** model, where a process creates several child processes, each with its own code (a fork), and then waits for the children to complete their execution (a join). Unfortunately, the name is confusing, because the UNIX system called **fork()** (studied shortly) is really an SPMD process creator, not a fork-join creator. We will, therefore refer to MPMD process creation rather than a fork-join creation. Note that Figure 13.4 is an example of MPMD programming (with m_kill_procs taking the place of the join).

An alternative view of process creation is to focus on the size of the code that can become a separate process. In some designs, individual statements can become processes and be executed in parallel. A second possibility is for procedures to be assigned to processes. This was the case in Figure 13.4, where the procedure multiply was assigned to processes via the call m_fork(multiply). A third possibility is for processes to represent whole programs only. Sometimes the different size of the code assignable to separate processes is referred to as the **granularity** of processes. The three choices of constructs for parallel execution that we have just listed could be described as follows:

+   1. Statement-level parallelism: fine-grained
+   2. Procedure-level parallelism: medium-grained
+   3. Program-level parallelism: large-grained

Granularity can be an issue in program efficiency: Depending on the kind of machine, many small-grained processes can incur significant overhead in their creation and management, thus executing more slowly than fewer larger processes. On the other hand, large-grained processes may have difficulty in exploiting all opportunities for parallelism within a program. An intermediate case that can be very efficient is that of a thread, which typically represents fine-grained or medium-grained parallelism without the overhead of full-blown process creation.

Regardless of the method of process creation, it is possible to distinguish between process creator (the parent process) and process created (the child process), and for every process creation mechanism, the following two questions must be answered:

+   1. Does the parent process suspend execution while its child processes are executing, or does it continue to execute alongside them?
+   2. What memory, if any, does a parent share with its children or the children share among themselves?

In Figure 13.4, the assumption was that the parent process suspends execution while the child processes compute. It was also necessary to indicate explicitly that the global variables a, b, and c are to be shared by all processes, using the keyword shared.

In addition to process creation, a parallel programming language needs a method for process termination. In the simplest case, a process will simply execute its code to completion and then cease to exist. In more complex situations, however, a process may need to continue executing until a certain condition is met and then terminate. It may also be necessary to select a particular process to continue execution.

We will briefly study process creation and destruction mechanisms for each kind of granularity.