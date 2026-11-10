the list of current clients is cached (compare the two *S* to *DB* curves). More strikingly, the bandwidth from the database to the server increases quadratically with the number of clients. By caching the list of users, we have reduced a quadratic increase into a linear increase (compare the two *DB* to *S* curves). This proves that the database can be a central bottleneck and that caching can be an effective strategy.

# ### 7.6.2 Experiment 2: Scaling Up the Number of Players

The experimental results reported in this section are based on our RCAT reference application, the multiplayer online jigsaw puzzle.

# #### 7.6.2.1 Experimental Setup

Because all players must know about the jigsaw pieces that all other players are acting on, we let TCP delay and piggyback the transmission of ACKs (TCP_QUICKACK socket flag kept at 0). We keep the default value of 40 ms of delay before sending an ACK.[^1] We also enable Nagle's algorithm (TCP_NO_DELAY socket flag kept at 0). The bots, proxies, and servers apply Nagle's algorithm and delayed ACKs.

The bots follow a scripted behavior. On both machines, a new bot joins the game every 10 seconds. Each bot starts by grabbing one piece and moves it by several game units X times per second, with X a configurable parameter. This bot behavior results in no piece having to be relocated between caches. We acknowledge that with real users, piece relocations will happen. However, unless many users fight for the same piece, these relocations should happen relatively rarely. We stop the script manually when we observe that the CPU capacity of the proxies or game servers is completely used. For example, the sum of the CPU capacity of the proxies may reach 400% if there are four proxies. However, Tornado recommends offloading tasks consuming considerable CPU to a thread pool. In our case, the game server keeps processing messages through Tornado, but offloads the game logic tasks to other threads. Consequently, the CPU for a single game server may reach more than 100% if the game logic threads are allocated to another core.

Bots measure the round-trip-time latency (latency, for short) using game messages containing globally unique identifiers. Each proxy and game server instance measures its (user plus system) CPU consumption, and the frequency of voluntary and involuntary context switches every

[^1]: See http://hwn.net/Articles/502585/.