# LOCK-BASED CONCURRENT DATA STRUCTURES

![](bbox=[0.233, 0.173, 0.703, 0.413])

Figure 29.11: Scaling Hash Tables

changes; that enabling more concurrency does not necessarily increase performance; that performance should only be remedied once they exist. This last point, of avoiding premature optimization, is central to any performance-minded developer; there is no value in making something faster doing so will not improve the overall performance of the application.

Of course, we have just scratched the surface of high performance structures. We see M and Shavi's excellent survey for more information, as well as links to other sources [MS04]. In particular, you might be interested in other structures (such as B-trees); for this knowledge, a database class is your best bet. You might also be interested in techniques that don't use traditional locks at all; such non-blocking data structures are something we'll get a taste of in the chapter on common concurrency bugs, but frankly this topic is an entire area of knowledge requiring more study than is possible in this humble book. Find out more on your own if you are interested (as always!).

© 2008–19, RPCACI-DUSSEAU