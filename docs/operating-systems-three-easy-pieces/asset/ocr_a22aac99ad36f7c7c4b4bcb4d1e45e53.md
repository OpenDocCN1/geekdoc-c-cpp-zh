# FILE SYSTEM IMPLEMENTATION

533

> TIP: UNDERSTAND STATIC VS. DYNAMIC PARTITIONING
When dividing a resource among different clients/users, you can use either static partitioning or dynamic partitioning. The static approach simply divides the resource into fixed proportions once; for example, if there are two possible users of memory, you can give some fixed fraction of memory to one user, and to the other. The dynamic approach is more flexible, giving out different amounts of the resource over time; for a period of time, but then later, the system may switch and decide to give a different user a larger share of disk bandwidth.

Each approach has its advantages. Static partitioning ensures each user receives some share of the resource, usually delivers more predictable performance, and is often easier to implement. Dynamic partitioning can achieve better utilization (by letting resource-hungry users consume other idle resources), but can be more complex to implement, and can lead to worse performance for users whose idle resources get consumed by others and take a long time to reclaim when needed. As often case, there is no best method; rather, you should think about the problem and decide which approach is most suitable. Indeed, shouldn't you always be doing that?

© 2008–19, ARPACI-DUSSEAU

THREE
ASY
PIECES