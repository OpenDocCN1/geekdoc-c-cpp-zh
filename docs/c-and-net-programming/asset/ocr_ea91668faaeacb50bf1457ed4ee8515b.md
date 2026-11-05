In C#, System.Threading.Thread.Priority is an enumeration that defines the priority states of a thread that in turn determines how much processor time a thread gets to execute.

+   3. **High priority** threads always get more processor time than their counterparts. If there is more than one thread at a high priority then the operating system cycles through the threads giving each high priority thread some amount of processor time. Lower priority threads do not get to execute as long as a higher priority thread is available.
+   
+   4. When there are no more threads of higher priority, the operating system then selects the next lower priority threads for execution. If at any point it encounters a higher priority thread, then the lower priority threads are preempted (taken away from CPU) and higher priority thread is executed.
+   
+   5. Any new thread when created, is assigned a **Normal priority.** If required the thread priority value can be changed to any of the values shown below. There are **5 priorities** defined in the Priority property of the Thread class.
+   
+       1. Highest
+       2. AboveNormal
+       3. Normal
+       4. BelowNormal
+       5. Lowest
+   
+   6. Syntax

```
    thread.Priority = ThreadPriority.Lowest
    //Example

    //Illustration of thread creation without setting any priority

    /* PrioritiesDemo1 program do not define any priority, which executes the method Show()
       first and then Main method gets a chance to execute. */

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading;

    namespace MultiThread
    {
        class PrioritiesDemo1
        {
            static void Main(string[] args)
            {
                Thread th = new Thread(Show);
```