proceed, it becomes blocked again. If no other thread calls signal again, the system deadlocks.

> > **CAUTION:**
> > A thread can only call await, signalAll, or signal on a condition if it owns the lock of the condition.

If you run the sample program in Listing 12.4, you will notice that nothing ever goes wrong. The total balance stays at $100,000 forever. No account ever has a negative balance. (Again, press Ctrl+C to terminate the program.) You may also notice that the program runs a bit slower—that is the price you pay for the added bookkeeping involved in the synchronization mechanism.

In practice, using conditions correctly can be quite challenging. Before you start implementing your own condition objects, you should consider using one of the constructs described in Section 12.5, “Thread-Safe Collections,” on p. 797.

**Listing 12.4** synch/Bank.java

```
```java
package synch;

import java.util.*;
import java.util.concurrent.locks.*;

/**
 * A bank with a number of bank accounts that uses locks for
serializing access.
 */
public class Bank10 {
    private final double[] accounts;
    private Lock bankLock;
    private Condition sufficientFunds;
}
```
```