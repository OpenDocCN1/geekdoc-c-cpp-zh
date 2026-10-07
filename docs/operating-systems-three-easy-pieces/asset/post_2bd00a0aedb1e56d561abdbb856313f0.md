
# COMMON CONCURRENCY PROBLEMS

The code here updates the next pointer to point to the current head, and then tries to swap the newly-created node to position as the new head of the list. However, this will fail if some other thread successfully swapped a new head in the meantime, causing this thread to retry with the new head.

Of course, building a useful list requires more than just a list insert, and not surprisingly building a list that you can insert, delete, and perform lookups on a lock-free manner is non-trivial. Read the recent literature on lock-free and wait-free synchronization to learn more [H01, H91, H93].

# Deadlock Avoidance via Scheduling

Instead of deadlock prevention, in some scenarios deadlock avoidance is preferable. Avoidance requires global knowledge of locks which various threads might grab during their execution, and schedules threads in a way to guarantee no deadlock can occur.

For example, we have two processors and four threads which must be scheduled upon time. Assume further that Thread 1 (T1) grabs L1 and L2 (in order, at some point during its execution), T2 grabs L1 and L2, as T3 just grabs L2, and T4 grabs locks at all. We can show these lock acquisition demands of the threads in table form:

| | T1 | T2 | T3 | T4 |
|---|---|---|---|---|
| L1 | yes | yes | no | no |
| L2 | yes | yes | yes | no |

A smart scheduler could compute that long as T1 and T2 are not at the same time, no deadlock could ever arise. Here is one such schedule:

| | T3 | T4 |
|---|---|---|
| CPU 1 | | |
| CPU 2 | | |

Note that it is OK for (T3 and T1) or (T3 and T2) to overlap. Even though T3 grabs L2, it can never cause a deadlock by running currently with other threads because it only grabs one lock.

Let's look at one more example. In this one, there is more contention for the same- resources (again, locks L1 and L2), as indicated by the following contention table:

| | T1 | T2 | T3 | T4 |
|---|---|---|---|---|
| L1 | yes | yes | yes | no |
| L2 | yes | yes | yes | no |

# COMMON CONCURRENCY PROBLEMS

TIP: DON'T ALWAYS DO IT PERFECTLY (TOM WEST'S LAW)
Tom West, as the subject of the classic computer-industry book Soul of a New Machine [K81], says famously: “Not everything worth doing is worth well”, which is a terrific engineering maxim. If a bad thing happens rarely, certainly one should not spend a great deal of effort to prevent it, particularly the cost of the bad thing is small. If, on the other hand, you are building a space shuttle, blowing up, well perhaps you should ignore this piece of advice.

Some readers object: “This sounds like you are suggesting mediocrity as a solution!” Perhaps they are right, that we should be careful with advice such as this. However, our experience tells us that in the world of engineering, with pressing deadlines and other real-world concerns, one will always have to decide which aspects of a system to build well and which to put aside for another. The hard part is knowing which to do when, a bit of insight gained through experience and dedication to the task at hand.

In particular, threads T1, T2, and T3 all need to grab locks L1 and L2 at some point during their execution. Here is a possible schedule that guarantees no deadlock could ever occur:

| CPU 1 | T4 |
| CPU 2 | T1 T2 T3 |

As you can see, static scheduling leads to a conservative approach where T1, T2, and T3 are all run on the same processor, and thus the total time to complete the jobs is lengthened considerably. Though it might have possible to run these tasks concurrently, the fear of deadlock prevents us from doing so, and the cost is performance.

One example of an approach like this is Dijkstra's Banker's Algorithm [D64], and many similar approaches have been described in the literature. Unfortunately, they are only useful in very limited environments, for an embedded system where one has full knowledge of the set of tasks that must be run and the locks that they need. Further, such approaches can limit concurrency, as we saw in the second example above. Thus, avoidance of deadlock via scheduling is not a widely-used general-purpose solution.

# Detect and Recover

One final general strategy is to allow deadlocks to occasionally occur, and then take some action once a deadlock has been detected. For example, if an OS froze once a year, you would just reboot it and get happily (or grumpily) on your work. If deadlocks are rare, such a non-solution is indeed quite pragmatic.

Many database systems employ deadlock detection and recovery techniques. A deadlock detector runs periodically, building a resource graph and checking it for cycles. In the event of a cycle (deadlock), the system needs to be restarted. If more intricate repair of data structures is required, a human being may be involved to ease the process.

More detail on database concurrency, and related issues can be found elsewhere [B+87, K87]. Read these works, or better yet, take a course on databases to learn more about this and interesting topic.

# 32.4 Summary

In this chapter, we have studied the types of bugs that occur in concurrent programs. The first type, atomicity bugs, are surprisingly common, and order violations, in which order was not. We have also discussed deadlock, as old as itself. The hard part is knowing which to do when, a bit of insight gained through experience and dedication to the task at hand.

In particular, threads T1, T2, and T3 all need to grab locks L1 and L2 at some point during their execution. Here is a possible schedule that guarantees no deadlock could ever occur:

As you can see, static scheduling leads to a conservative approach where T1, T2, and T3 are all run on the same processor, and thus the total time to complete the jobs is lengthened considerably. Though it might have possible to run these tasks concurrently, the fear of deadlock prevents us from doing so, and the cost is performance.

One example of an approach like this is Dijkstra's Banker's Algorithm [D64], and many similar approaches have been described in the literature. Unfortunately, they are only useful in very limited environments, for an embedded system where one has full knowledge of the set of tasks that must be run and the locks that they need. Further, such approaches can limit concurrency, as we saw in the second example above. Thus, avoidance of deadlock via scheduling is not a widely-used general-purpose solution.

In this chapter, we have studied the types of bugs that occur in concurrent programs. The first type, atomicity bugs, are surprisingly common, and order violations, in which order was not. We have also discussed deadlock, as old as itself. The hard part is knowing which to do when, a bit of insight gained through experience and dedication to the task at hand.

In this chapter, we have studied the types of bugs that occur in concurrent programs. The first type, atomicity bugs, are surprisingly common, and order violations, in which order was not. We have also discussed deadlock, as old as itself. The hard part is knowing which to do when, a bit of insight gained through experience and dedication to the task at hand.

# COMMON CONCURRENCY PROBLEMS

# References

- **B+87**: "Deadlock Detection in Distributed Databases" by Edgar Knapp. ACM Computing Systems, 20:3, 1987. An introduction to distributed systems. Points to a number of related works, and this is a good place to start your reading.
- **D-64**: "Algorithm for ordering" by Edsger Dijkstra. 1964. Available: http://www.utexas.edu/users/deadlock.
- **G02**: "MapReduce: Implementing on Scale Clusters" by Sanjay Ghewat, Jeff Dean. OSD'04, San Francisco, October 2004. The MapReduce ushered in the era of large-scale data.
- **H01**: (Recent literature on lock-free and wait-free synchronization).
- **H91**: "Wait-free" by Maurice Herly. ACM TOPLAS, 13, January 1991. Herly's work explores the ideas behind wait-free.
- **K81**: "Soul of a New Machine" by Tracy Kidicker. Backbyte Books, 2000 (reprint of 1990). A must-read for any systems builder or engineer, detailing how a team inside, wait-free.
- **H93**: "A Methodology for Implementing Concurrent Objects" by Maurice Herly. ACM TOPLAS, 15:5, November 1993. A new overview of wait-free.
- **I08**: "Deadlock Immunity: Enabling Systems To Defend Against Deadlocks" by Horatu Juli, Daniel Tralam, Cristian Zamfir. OSD'08, San Diego, CA, December 2008. An excellent recent paper on deadlocks, and how to avoid getting caught in the ones and errors in a particular system.
- **L08**: "Learning from Mutexes — A Comprehensive Study of Real World Concurrency Bugs" by Chan Lu, Suoyey Park, Eunsoo Seo, Yuanyuan Zhou. OSLAS '08, March 2008, Seattle. The first in-depth study of concurrency bugs in real software, and the search for this chapter. Look at Y.Y. Shao's web pages for more interesting papers on bugs.
- **T+94**: "Time Memory Maps" by Tom West. We have read many others. Available, online at: http://lxr-free-electrons.com/source/filemap.c. Thanks to Michael Walsh (NY) for pointing out this example. The real world, as you see in this file, be a bit more complex than the simple clarity found in textbooks...
