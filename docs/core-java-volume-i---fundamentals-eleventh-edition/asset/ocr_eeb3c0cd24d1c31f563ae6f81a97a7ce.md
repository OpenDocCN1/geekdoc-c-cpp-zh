![](bbox=[0.256, 0.154, 0.826, 0.606])

**Figure 12.4**  A deadlock situation

class. In the call to transfer, flip fromAccount and toAccount. Run the program and see how it deadlocks almost immediately.

Here is another situation in which a deadlock can occur easily. Change the signalAll method to signal in the SynchBankTest program. You will find that the program eventually hangs. (Again, set NACCOUNTs to 10 to observe the effect more quickly.) Unlike signalAll, which notifies all threads that are waiting for added funds, the signal method unblocks only one thread. If that thread can’t proceed, all threads can be blocked. Consider the following sample scenario of a developing deadlock:

+   1. Account 1: $1,990
+   2. All other accounts: $990 each