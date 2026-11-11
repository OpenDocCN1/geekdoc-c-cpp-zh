For a given number of steps, this thread transfers a random amount, and then sleeps for a random delay.

We need to catch an `InterruptedException` that the sleep method threatens to throw. We will discuss this exception in [Section 12.3.1, “Interrupting Threads,”](#) on p. 757. Typically, interruption is used to request that a thread terminates. Accordingly, our run method exits when an `InterruptedException` occurs.

Our program starts a second thread as well that moves money from account 2 to account 3. When you run this program, you get a printout like this:

```
Thread[Thread-1,5,main]  606.77 from 2 to 3 Total
Balance:  400000.00
Thread[Thread-0,5,main]   98.99 from 0 to 1 Total
Balance:  400000.00
Thread[Thread-1,5,main]  476.78 from 2 to 3 Total
Balance:  400000.00
Thread[Thread-0,5,main]  653.64 from 0 to 1 Total
Balance:  400000.00
Thread[Thread-1,5,main]  807.14 from 2 to 3 Total
Balance:  400000.00
Thread[Thread-0,5,main]  481.49 from 0 to 1 Total
Balance:  400000.00Thread[Thread-0,5,main]  203.73 from 0 to 1
Total Balance:  400000.00
Thread[Thread-1,5,main]  111.76 from 2 to 3 Total
Balance:  400000.00
Thread[Thread-1,5,main]  794.88 from 2 to 3 Total
Balance:  400000.00
. . .
```

As you can see, the output of the two threads is interleaved, showing that they run concurrently. In fact, sometimes the output is a little messier when two output lines are interleaved.

That’s all there is to it! You now know how to run tasks concurrently. The remainder of this chapter tells you how to control the interaction between threads.