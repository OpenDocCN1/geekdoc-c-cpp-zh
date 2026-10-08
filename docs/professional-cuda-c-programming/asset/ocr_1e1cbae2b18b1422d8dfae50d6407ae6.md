# # Bank Conflict

When multiple addresses in a shared memory request fall into the same bank, a bank conflict occurs, causing the request to be replayed. The hardware splits a request with a bank conflict into many separate conflict-free transactions as necessary, decreasing the effective bandwidth by a factor equal to the number of separate memory transactions.

Three typical situations occur when a request to shared memory is issued by a warp:

+   * **Parallel access**: multiple addresses accessed across multiple banks

+   * **Serial access**: multiple addresses accessed within the same bank

+   * **Broadcast access**: a single address read in a single bank

Parallel access is the most common pattern: multiple addresses accessed by a warp that fall into multiple banks. This pattern implies that some, if not all, of the addresses can be serviced in a single memory transaction. Optimally, a conflict-free shared access is performed when every address is in a separate bank.

Serial access is the worst pattern: When multiple addresses fall into the same bank, the request must be serialized. If 32 threads in a warp access different memory locations in a single bank, 32 memory transactions will be required and satisfying those takes 32 times as long as a single request.

In the case of broadcast access, all threads in a warp read the same address within a single bank. One memory transaction is executed, and the accessed word is broadcast to all requesting threads. While only a single memory transaction is required for a broadcast access, bandwidth utilization is poor because only a small number of bytes are read.

Figure 5-2 illustrates the optimal bank access pattern. Each thread accesses a 32-bit word. There is no bank conflict because each thread accesses an address in a different bank. Figure 5-3 illustrates an irregular, random access pattern. There is still no bank conflict, because each thread accesses a different bank. Figure 5-4 illustrates another irregular access pattern where several threads access the same bank. There are two possible behaviors for such a request:

+   * Conflict-free broadcast access if thread accesses the same address within a bank

+   * Bank conflict if thread accesses different addresses within a bank

![](bbox=[0.118, 0.735, 0.915, 0.91])