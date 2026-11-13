
## 6.4.1 The Selection Problem

The first problem we will examine is the selection problem from Section 1.1. Recall that the input is a list of N elements, which can be totally ordered, and an integer k. The selection problem is to find the kth largest element.

Two algorithms were given in Chapter 1, but neither is very efficient. The first algorithm, which we shall call algorithm 1A, is to read the elements into an array and sort them, returning the appropriate element. Assuming a simple sorting algorithm, the running time is O(N^2). The alternative algorithm, 1B, is to read k elements into an array and sort them. The smallest of these is the kth element. We process the remaining elements one by one. As an element arrives, it is compared with the kth element in the array. If it is larger, then the kth element is removed, and the new element is placed in the correct place among the remaining k - 1 elements. When the algorithm ends, the element in the kth position is the answer. The running time is O(N · k) (why?). If k = [N/2], then both algorithms are O(N^2). Notice that for any k, we can solve the symmetric problem of finding the (N - k + 1)th smallest element, so k = [N/2] is really the hardest case for these algorithms. This also happens to be the most interesting case, since this value of k is known as the median.

We give two algorithms here, both of which run in O(N log N) in the extreme case of k = [N/2], which is a distinct improvement.

### Algorithm 6A

For simplicity, we assume that we are interested in finding the kth smallest element. The algorithm is simple. We read the N elements into an array. We then apply the buildHeap algorithm to this array. Finally, we perform k deleteMin operations. The last element extracted from the heap is our answer. It should be clear that by changing the heap-order property, we could solve the original problem of finding the kth largest element.

The correctness of the algorithm should be clear. The worst-case timing is O(N) to construct the heap, if buildHeap is used, and O(log N) for each deleteMin. Since there are k deleteMins, we obtain a total running time of O(N + k · log N). If k = O(N/log N), then the running time is dominated by the buildHeap operation and is O(N). For larger values of k, the running time is O(k log N). If k = [N/2], then the running time is Θ(N log N).

Notice that if we run this program for k = N and record the values as they leave the heap, we will have essentially sorted the input file in O(N log N) time. In Chapter 7, we will refine this idea to obtain a fast sorting algorithm known as heapsort.

### Algorithm 6B

For the second algorithm, we return to the original problem and find the kth largest element. We use the idea from algorithm 1B. At any point in time we will maintain a set S of the k largest elements. After the first k elements are read, when a new element is read it is compared with the kth largest element, which we denote by S_k. Notice that S_k is the smallest element in S. If the new element is larger, then replaces S_k in S. S will then have a new smallest element, which may or may not be the newly added element. At the end of the input, we find the smallest element in S and return it as the answer.

This is essentially the same algorithm described in Chapter 1. Here, however, we will use a heap to implement S. The first k elements are placed into the heap in total time O(k) with a call to buildHeap. The time to process each of the remaining elements is O(1), to test if the element goes into S, plus O(log k), to delete $S_k$ and insert the new element if this is necessary. Thus, the total time is $O(k + (N-k) \log k) = O(N \log k)$. This algorithm also gives a bound of $\Theta(N \log N)$ for finding the median.

In Chapter 7, we will see how to solve this problem in $O(N)$ average time. In Chapter 10, we will see an elegant, albeit impractical, algorithm to solve this problem in $O(N)$ worst-case time.

## 6.4.2 Event Simulation

In Section 3.7.3, we described an important queuing problem. Recall that we have a system, such as a bank, where customers arrive and wait in a line until one of k tellers is available. Customer arrival is governed by a probability distribution function, as is the service time (the amount of time to be served once a teller is available). We are interested in statistics such as how long on average a customer has to wait or how long the line might be.

With certain probability distributions and values of k, these answers can be computed exactly. However, as k gets larger, the analysis becomes considerably more difficult, so it is appealing to use a computer to simulate the operation of the bank. In this way, the bank officers can determine how many tellers are needed to ensure reasonably smooth service.

A simulation consists of processing events. The two events here are (a) a customer arriving and (b) a customer departing, thus freeing up a teller.

We can use the probability functions to generate an input stream consisting of ordered pairs of arrival time and service time for each customer, sorted by arrival time. We do not need to use the exact time of day. Rather, we can use a quantum unit, which we will refer to as a tick.

One way to do this simulation is to start a simulation clock at zero ticks. We then advance the clock one tick at a time, checking to see if there is an event. If there is, then we process the event(s) and compile statistics. When there are no customers left in the input stream and all the tellers are free, then the simulation is over.

The problem with this simulation strategy is that its running time does not depend on the number of customers or events (there are two events per customer), but instead depends on the number of ticks, which is not really part of the input. To see why this is important, suppose we changed the clock units to milliseconds and multiplied all the times in the input by 1,000. The result would be that the simulation would take 1,000 times longer!

The key to avoiding this problem is to advance the clock to the next event time at each stage. This is conceptually easy to do. At any point, the next event that can occur is either (a) the next customer in the input file arrives or (b) one of the customers at a teller leaves. Since all the times when the events will happen are available, we just need to find the event that happens nearest in the future and process that event.

If the event is a departure, processing includes gathering statistics for the departing customer and checking the line (queue) to see whether there is another customer waiting. If so, we add that customer, process whatever statistics are required, compute the time when that customer will leave, and add that departure to the set of events waiting to happen.

If the event is an arrival, we check for an available teller. If there is none, we place the arrival on the line (queue); otherwise we give the customer a teller, compute the customer's departure time, and add the departure to the set of events waiting to happen.

The waiting line for customers can be implemented as a queue. Since we need to find the event nearest in the future, it is appropriate that the set of departures waiting to happen be organized in a priority queue. The next event is thus the next arrival or next departure (whichever is sooner); both are easily available.

It is then straightforward, although possibly time-consuming, to write the simulation routines. If there are C customers (and thus 2C events) and k tellers, then the running time of the simulation would be O(C log(k + 1)) because computing and processing each event takes O(log H), where H = k + 1 is the size of the heap.3

## 6.5 d-Heaps

Binary heaps are so simple that they are almost always used when priority queues are needed. A simple generalization is a d-heap, which is exactly like a binary heap except that all nodes have d children (thus, a binary heap is a 2-heap).

Figure 6.19 shows a 3-heap. Notice that a d-heap is much shallower than a binary heap, improving the running time of inserts to O(log_d N). However, for large d, the deleteMin operation is more expensive, because even though the tree is shallower, the minimum of d children must be found, which takes d - 1 comparisons using a standard algorithm. This raises the time for this operation to O(d log_d N). If d is a constant, both running times are, of course, O(log N). Although an array can still be used, the multiplications and divisions to find children and parents are now by d, which, unless d is a power of 2, seriously increases the running time, because we can no longer implement division by a bit shift. d-heaps are interesting in theory, because there are many algorithms where the number of insertions is much greater than the number of deleteMins (and thus a theoretical speedup is possible). They are also of interest when the priority queue is too large to fit entirely in main memory.

![](img/e449061a0cac9cafaefd979fab665b33_278_0.png)

Figure 6.19 A d-heap (d = 3)
