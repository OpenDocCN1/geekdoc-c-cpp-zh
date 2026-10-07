# 246 Performance, Reliability, and Availability Evaluation of Computational Systems

balancer delivers (4) the request to the least loaded server (5). The HTTP transaction is processed in the server, and a reply (6) is sent to the user through the local network (7) and the internet (8). The load balancer periodically requests information related to resource usage from the servers ($r_1$, and $r_2$). If the server $j$ is alive, it replies, providing the information requested ($i_j, j=\{1, 2\}$).

# Active-Active

![](bbox=[0.196, 0.237, 0.802, 0.432])

Two Servers Available and Processing 100% of the Workload Being Processed.

# Figure 21.31 Active-Active Servers - Processing 100%.

When the server is unavailable, it does not reply (see Figure 21.32). The load balancer, waits for a reply during a specified period. In the time being, keeps forwarding HTTP requests to the server. If the server is unavailable, these requests are lost. Assuming the load balancer evenly distributes the requests among both servers, 50% of the requests are lost.

After the specified delay, the load balancer understands the server is not available and stops forwarding HTTP requests to that (see Figure 21.33). Now, 100% of the HTTP requests are handled by the only available server. It is worth stressing that although 100% of the requests are covered, the processing capacity is reduced to only one server. The load balancer resumes requests requests to the unavailable when it replies to the information. In this state, the system is again coping with the HTTP request, and it has two servers processing the requests (see Figure 21.31).

Figure 21.34 presents a CTMC that is an availability model of the system depicted in Figure 21.30. In state $S_0$ both servers are available and processing HTTP requests. A failure may occur with a rate of $2A$, and such a failure may be covered with probability $c$ or stay hidden with probability $(1-c)$. It is worth noting that the probability $c$ represents the failure detection mechanism's capacity to sense a failure incident. If the failure is detected, the system transitions to state $S_1$ and otherwise, to state $S_3$. In both states, $S_1$ and $S_3$, only one server is available,