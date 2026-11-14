Observe that in the entry section of the critical section, if the entering task is not the only reader, then there must already be other readers. Such a condition implies there cannot be any writers. Otherwise, one must check to ensure that there are no writers before proceeding.

If a writer is in the critical section, n readers are waiting, one reader is queued on wrtSem, n – 1 readers are queued on mutex, and if a writer executes signal(wrtSem), it may resume the waiting readers or one waiting writer. The decision is made by the scheduler.

The tacit assumption being made is that the buffers that are being written to or read from are managed to ensure that neither underflow nor overflow occurs.

# 12.10 MONITORS

The semaphores we have studied are a fundamental method for synchronization. However, they are a low-level mechanism and it is easy to make errors with them. An alternative solution uses a data type called a monitor. Monitors are program modules that offer more structure than semaphores, with an implementation that can be as efficient.

A monitor is a data abstraction mechanism that encapsulates a representation of an abstract object. The monitor provides a public interface as the only means by which internal data may be manipulated. Note that this is similar to a class in either C++ or Java. The monitor contains an internal (private) variable to store the object’s state and Procedures (methods or function members) that implement the operations on the object. Mutual exclusion is satisfied by ensuring that procedures in the same monitor cannot execute simultaneously. Conditional synchronization is provided through condition variables.

A monitor is used to group a representation and implementation of a shared resource. It has an interface and a body. The (public) interface specifies those operations provided by the resource, while the body contains variables that represent the state of the resource. Internal procedures implement the operations specified in the interface. The monitor can be schematically illustrated as shown in Figure 12.45.

```
monitor monName
{
initialization statements
procedures
permanent variables
}
```

Figure 12.45 The Monitor – A Typical Structure.

The procedures implement the visible operations. All processes in the monitor share the permanent variables. They are denoted permanent because they retain their values on exit as long as the monitor exists. Such behavior occurs in C or C++ with static variables. The procedures may also have local variables.

By virtue of being an abstract data type (ADT), the monitor is a distinct scope. Only the procedure names are visible outside of the monitor – the public interface. Permanent variables can only be changed through one of the visible procedures. Statements within the monitor cannot affect variables outside the monitor, that is, those in a different scope. Permanent variables are initialized before any procedure is called. The initialization is accomplished by executing initialization procedures when the monitor instance is created.