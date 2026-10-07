# 48 Performance, Reliability, and Availability Evaluation of Computational Systems

17.6.a). Nevertheless, $WS_2$ is operational and can assume the transaction processing as soon as transactions are delivered to it; that is, $WS_2$ is turned on and available.

This redundant strategy is usually **hot-standby** sparing. The difference between hot-standby and active-active is that in the former, the second server ($WS_2$) does not process transactions while the primary server ($WS_1$) is active, whereas, in the latter, requests are sent to both servers. In the hot-standby strategy, when the active server ($WS_1$) fails, the erroneous state may be detected or not. If the erroneous state is detected, the spare server ($WS_2$) immediately assumes the total workload (Figure 17.6.c).

![](bbox=[0.225, 0.305, 0.775, 0.785])

**Figure 17.6** Hot-Standby.

However, if the erroneous state is not detected, the load balancer keeps sending the requests to the faulty server (Figure 17.6.b); thus causing a significant impact on the