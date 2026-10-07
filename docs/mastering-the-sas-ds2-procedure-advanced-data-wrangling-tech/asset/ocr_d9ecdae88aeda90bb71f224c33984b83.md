It is also clear from the log that although three threads were spawned, threads 1 and 2 didn't process any data. Because cls.banks is very small, there was really only one block of data, and therefore all of the data was sent to thread 0. Threads 1 and 2 executed and terminated without processing any data.

When executing DS2 on the SAS compute platforms with realistically sized data, I visualize the process as shown in Figure 6.2.

# **Figure 6.2: DS2 Threaded Processing on the SAS Compute Platform**

![](bbox=[0.215, 0.252, 0.833, 0.558])

The SET statement spawns a single read thread that distributes the source data to the prescribed number of threads. The single read thread ensures that a row of data is never passed to more than one thread. As each thread completes its computations on a row of data, and returns the result to the data program's PDV. The data program processes the row and writes it to the target data set in a single-threaded process.

# 6.3.2 Parallel Processing Data with DS2 Threads

When you are considering whether threading DS2 on the SAS compute platform will improve performance, ask these two primary questions:

+   - Is the process CPU bound? If the process is I/O bound we have to remember that there will be only one read thread for our process and adding additional threads will probably actually degrade performance, not improve it.
- Is the data set are large enough to produce several blocks that can be distributed to more than one thread? Even if the process is CPU bound, if the data is small that all gets sent to a single compute thread, we shouldn't expect improved performance

We have access to a DS2 package containing a scoring method and a DS2 data program that is currently used for scoring. We've been asked to convert this to a threaded process. The data set that we are scoring is cr.campaign.