given system. Also, qk (k = 1, 2) represents the probabilities that a processor requests a direct memory access. If both processors are accessing two different memory modules (in this case, the system stays in state (1, 1)) and will complete the task by the end of this memory cycle, then the expectation of the number of memory requests completed in this memory cycle is 2. If there are two requests to access memory module 1 in a memory cycle, then only one request can be completed in this memory cycle. We can obtain the same expectation when memory module 2 is requested to be accessed. We denote the random variable Y as the number of requests completed in every memory cycle in the steady state and the request state space is the set { 0, 1, 2 }. The conditional expectations of Y can be mathematically described as:

+   E [ Y | system in state (1, 1) ] = 2;
+   E [ Y | system in state (2, 0) ] = 1;
+   E [ Y | system in state (0, 2) ] = 1.

In order to analyze the performance of such a system, we are interested in learning the steady probabilities of the states, in which the memory modules are efficiently used, and the expected number of memory requests satisfied in each memory cycle in the steady state.

![](bbox=[0.14, 0.56, 0.8, 0.85])