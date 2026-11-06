# 23.2 The ‘fork’ system call

From the C programming language the fork system call is well known. When a program needs to start a new process, system can be used. The fork system requires the program to wait for the *child process* to terminate. The more general way to spawn subprocesses is to use `fork`.

In this section we investigate how C++ can be used to wrap classes around a complex system call like `fork`. Much of what follows in this section directly applies to the Unix operating system, and the discussion therefore focuses on that operating system. Other systems usually provide comparable facilities. What follows is closely related to the *Template Design Pattern* (cf. *Gamma et al.* (1995) Design Patterns, Addison-Wesley)

When fork is called, the current program is duplicated in memory, thus creating a new process. Following this duplication both processes continue their execution just below the fork system call. The two processes may inspect fork’s return value: the return value in the original process (called the *parent process*) differs from the return value in the newly created process (called the *child process*):

+   - In the *parent process* `fork` returns the *process ID* of the (child) process that was created by the `fork` system call. This is a positive integer value.
+   - In the *child process* `fork` returns 0.
+   - If `fork` fails, -1 is returned.

# 23.2.1 A basic Fork class

A basic `Fork` class should hide all bookkeeping details of a system call like `fork` from its users. The class `Fork` developed here does just that. The class itself only ensures the proper execution of the `fork` system call. Normally, `fork` is called to start a child process, usually boiling down to the execution of a separate process. This child process may expect input at its standard input stream and/or may generate output to its standard output and/or standard error streams. `Fork` does not know all this, and does not have to know what the child process will do. `Fork` objects should be able to start their child processes.

Fork’s constructor cannot know what actions its child process should perform. Similarly, it cannot know what actions the parent process should perform. For these kind of situations, the *template method design pattern* was developed. According to Gamma c.s., *the template method design pattern*

> “Define(s) the skeleton of an algorithm in an operation, deferring some steps to subclasses. [The] Template Method (design pattern) lets subclasses redefine certain steps of an algorithm, without changing the algorithm’s structure.”

This design pattern allows us to define an *abstract base class* already providing the essential steps related to the `fork` system call, deferring the implementation of other parts of the `fork` system call to subclasses.

The `Fork` abstract base class has the following characteristics:

+   - It defines a data member `d_pid`. In the parent process this data member contains the child’s *process id* and in the child process it has the value 0. Its public interface declares only two members:
+     - a `fork` member function, responsible for the actual forking (i.e., it creates the (new) child process);
+     - a `virtual` destructor `~Fork` (having an empty body).

Here is Fork’s interface:

```
class Fork
```