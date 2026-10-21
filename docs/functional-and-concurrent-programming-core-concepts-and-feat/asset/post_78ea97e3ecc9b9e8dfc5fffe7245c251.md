
12.11 All the solutions to subset-sum; contrast with Lis. 12.10 and 12.12. 192

12.12 The solutions to subset-sum derived lazily; contrast with Lis. 12.11. 192

13.1 Pipeline example with no handling of failures; contrast with Lis. 13.2. 201

13.2 Pipeline example with failure handling; contrast with Lis. 13.1. 202

14.1 Example of non-optimized tail-calls; contrast with Lis. 14.3. 205

14.2 Trampoline for tail-call optimization in Scala. 206

14.3 Optimized tail-calls, using a trampoline; contrast with Lis. 14.1. 207

14.4 Trampoline for tail-call optimization in Java. 208

14.5 Optimized tail-calls, using a trampoline, Java variant. 208

14.6 Trampoline extended with map and flatMap. 211

14.7 Non-tail recursive factorial, as a trampoline; see also Lis. 14.10. 212

14.8 Non-tail recursive size on trees, as a trampoline; see also Lis. 14.10. 212

14.9 Non-tail recursive hanoi, as a trampoline; see also Lis. 14.10. 212

14.10 For-yield on trampolines; contrast with Lis. 14.7 to 14.9. 213

15.1 Example of ad hoc polymorphism. 232

15.2 Example of parametric polymorphism. 233

15.3 Example of subtype polymorphism; see also Lis. 15.4. 233

15.4 Using subtype polymorphism to process a heterogeneous collection. 234

15.5 Example of a user-defined covariant type. 238

15.6 Example of a user-defined contravariant type. 239

15.7 Example of an upper type bound for use-site variance. 241

15.8 Example of a lower type bound for use-site variance. 242

15.9 Example of a type parameter with both lower and upper bounds. 242

15.10 Example of a combined upper type bound; contrast with Lis. 15.14. 243

## List of Listings
- 19.1 Example of threads freely sharing immutable objects. 285
- 19.2 Safe list that encapsulates synchronization; contrast with Lis. 18.5. 287
- 19.3 Example of client-side locking. 289
- 19.4 Safe list based on a private lock; contrast with Lis. 19.2. 290
- 19.5 Safe list based on an immutable list; contrast with Lis. 19.2 and 19.4. 291
- 19.6 Safe list with an immutable list/private lock; contrast with Lis. 19.5. 293
- 20.1 Thread-safe queue (single public lock); see also Lis. 20.5 and 20.7. 298
- 20.2 Batch insertions by client-side locking on a concurrent queue. 299
- 20.3 Batch extraction by client-side locking on a concurrent queue. 300
- 20.4 Batch extraction without synchronization; contrast with Lis. 20.3. 300
- 20.5 Thread-safe queue (single private lock); see also Lis. 20.1 and 20.7. 301
- 20.6 Batch processing from queue with a private lock. 302
- 20.7 Thread-safe queue (two private locks); see also Lis. 20.1 and 20.5. 303
- 20.8 Batch processing from a queue with a split lock. 304
- 21.1 Example concurrency from a thread pool; contrast with Lis. 17.1. 307
- 21.2 Using a thread pool to create threads and wait for their termination. 309
- 21.3 A server that processes requests sequentially; contrast with Lis. 21.4. 310
- 21.4 A server that processes requests concurrently; contrast with Lis. 21.3. 310
- 21.5 Example of scheduled execution using a timer pool. 313
- 21.6 Example of parallel evaluation of higher-order function map. 316
- 22.1 Threads from a pool share a safe list. 321
- 22.2 Waiting for task completion using a countdown latch synchronizer. 325
- 22.3 Deadlock-prone implementation of a box; fixed in Lis. 22.4. 326
- 22.4 Thread-safe box with a latch; fixed from Lis. 22.3; see also Lis. 27.2. 327
- 22.5 First variant for method set from Lis. 22.4. 328
- 22.6 Second variant for method set from Lis. 22.4. 328
- 22.7 Example of events tied and not tied by happens-before; see Fig. 22.4. 332
- 22.8 Possible implementation of get in Lis. 22.4 and 22.6. 334
- 23.1 Variant of Lis. 18.7 with a timeout. 337
- 23.2 Example use of a read-write lock. 338
- 23.3 Add latches to Lis. 21.2 for increased concurrency and precise timing. 339
- 23.4 Replace two latches from Lis. 23.3 with a single barrier. 340
- 23.5 Simple lock implementation using a semaphore. 341
- 23.6 Bounded queue based on two semaphores; see also Lis. 23.7 and 23.8. 342
- 23.7 Bounded queue with a single condition; see also Lis. 23.8. 343
- 23.8 Bounded queue based on two conditions. 345
- 23.9 Searching files and storing results as a producer–consumer pattern. 353
- 24.1 Parallel execution: one new thread per task. 356
- 24.2 Parallel execution: bounded number of threads. 358
- 24.3 Parallel execution: dedicated thread pool. 359
- 24.4 Parallel execution: shared thread pool. 360

## List of Listings
- 24.5 Parallel execution: shared thread pool with a bound. 361
- 24.6 Parallel execution: parallel collections. 362
- 24.7 Extensible parallel execution using a single condition. 363
- 24.8 Extensible parallel execution using two conditions. 366
- 24.9 Extensible parallel execution using two semaphores. 367
- 25.1 Value-producing tasks handled as futures. 371
- 25.2 A parallel server with parallelism within responses; see also Lis. 26.8. 373
- 25.3 Dealing with a future’s timeout and failure. 374
- 25.4 Possible implementation of Future.apply; see also Lis. 25.5 and 25.6. 376
- 25.5 Future creation from a CompletableFuture promise. 376
- 25.6 Future creation from a FutureTask promise. 377
- 25.7 A thread-safe memoization function, using promises and futures. 379
- 26.1 Deadlock-prone parallel quick-sort; see also Lis. 26.5. 381
- 26.2 Ad-fetching example; contrast with Lis. 26.3, 26.6, and 26.7. 383
- 26.3 Ad-fetching example with a callback on a future. 385
- 26.4 Reimplementing higher-order function map on futures. 387
- 26.5 Non-blocking implementation of parallel quick-sort. 389
- 26.6 Ad-fetching example with map and foreach on futures. 390
- 26.7 Ad-fetching example with flatMap and foreach on futures. 390
- 26.8 A fully non-blocking parallel server. 390
- 26.9 A pipeline of futures using flatMap. 394
- 26.10 Joining a list of CompletableFutures into one without blocking. 396
- 27.1 Conceptual implementation of class AtomicInteger in Java. 400
- 27.2 Thread-safe box with a latch and no lock. 401
- 27.3 Lock-free implementation of a thread-safe stack (Treiber’s algorithm). 403
- 27.4 Example of non-blocking concurrency using ForkJoinPool. 405
- 27.5 Example of non-blocking concurrency with an async/await construct. 406
- 27.6 Example of non-blocking concurrency using Kotlin coroutines. 407
- 27.7 Example of non-blocking concurrency using actors. 408
- 27.8 Example of a state machine as an actor that switches behavior. 410
- 27.9 Example of non-blocking transformation using reactive streams. 411
- 28.1 A sequential runner of strategies with timeout. 419
- 28.2 A parallel runner of strategies based on invokeAny. 421
- 28.3 A parallel runner of strategies based on CompletionService. 422
- 28.4 Extending Scala futures with completeOnTimeout. 423
- 28.5 Earliest Scala future that satisfies a condition; see also Lis. 28.7. 424
- 28.6 A parallel asynchronous runner of strategies using Scala futures. 425
- 28.7 Earliest CompletableFuture that satisfies a condition. 426
- 28.8 Asynchronous runner variant based on CompletableFuture. 427
- 28.9 Asynchronous runner with thread-safe caching. 428

## List of Figures
- 3.1 Functional lists memory sharing. 32
- 5.1 true ∧ (false ∨ ¬(true ∧ false)) as a tree. 53
- 6.1 Tower of Hanoi problem. 66
- 7.1 Recursive strategy for function drop. 82
- 7.2 Data sharing between list and drop(list, n). 83
- 7.3 Data copying between list and take(list, n). 85
- 7.4 Recursive strategy for function concat. 86
- 7.5 Recursive strategy for function flatten. 87
- 8.1 A binary search tree. 100
- 8.2 The binary search tree from Figure 8.1 after key 57 is removed. 105
- 8.3 Tree rotations. 109
- 11.1 A file system tree and its string representation. 159
- 15.1 Subtype relationship of two functions. 240
- 18.1 Possible interleaving of two increment operations. 273
- 18.2 Possible interleaving of two non-atomic compound actions. 275
- 18.3 Possible interleaving of two non-atomic check-then-act. 276
- 19.1 Possible interleaving of three SafeStringList.add operations. 292
- 19.2 Semantics of concurrency as interleaving of atomic actions. 294
- 20.1 FIFO queue implemented as two LIFO lists. 297
- 20.2 Possible interleaving of two ConcurrentQueue.take operations. 299
- 20.3 Possible deadlock due to an incorrect drain implementation in ConcurrentQueue. 305
- 22.1 Possible deadlock of the incorrect box implementation in Lis. 22.3. 327
- 22.2 Single-threaded executions are sequentially consistent. 330
- 22.3 Multithreaded executions are not sequentially consistent. 331
