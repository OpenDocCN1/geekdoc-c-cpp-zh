```
Running total for Child #1 is 15
Running total for Child #2 is 19
Running total for Child #1 is 24
Running total for Child #2 is 29
Sum for Child #1 is 29
Child #1 terminating.
Sum for Child #2 is 29
Child #2 terminating.
```

As the output shows, both child threads are using SumIt() at the same time on the same object, and the value of sum is corrupted.

The effects of lock are summarized here:

+   - For any given object, once a lock has been acquired, the object is locked and no other thread can acquire the lock.
+   - Other threads trying to acquire the lock on the same object will enter a wait state until the code is unlocked.
+   - When a thread leaves the locked block, the object is unlocked.

# An Alternative Approach

Although locking a method's code, as shown in the previous example, is an easy and effective means of achieving synchronization, it will not work in all cases. For example, you might want to synchronize access to a method of a class you did not create, which is itself not synchronized. This can occur if you want to use a class that was written by a third party and for which you do not have access to the source code. Thus, it is not possible for you to add a lock statement to the appropriate method within the class. How can access to an object of this class be synchronized? Fortunately, the solution to this problem is simple: Lock access to the object from code outside the object by specifying the object in a lock statement. For example, here is an alternative implementation of the preceding program. Notice that the code within SumIt() is no longer locked and no longer declares the lockOn object. Instead, calls to SumIt() are locked within MyThread.

```
// Another way to use lock to synchronize access to an object.

using System;
using System.Threading;

class SumArray {
    int sum;
    public int SumIt(int[] nums) {
        sum = 0; // reset sum

        for(int i=0; i < nums.Length; i++) {
            sum += nums[i];
            Console.WriteLine("Running total for " +
                Thread.CurrentThread.Name +
                " is " + sum);
            Thread.Sleep(10); // allow task-switch
        }
        return sum;
```