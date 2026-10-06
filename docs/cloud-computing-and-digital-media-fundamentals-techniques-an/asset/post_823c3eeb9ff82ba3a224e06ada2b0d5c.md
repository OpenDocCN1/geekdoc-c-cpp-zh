
# Resource Optimization for Multimedia Cloud Computing ■ 33

server, and the bandwidth resource at the transmission server, subject to the queuing stability constraint in each queuing system and the resource cost constraint. Mathematically, the problem can be formulated as follows:

```
$M \in minimize \frac{T^{tot(t)}}{FCFS} (S^t_1, \dots, S^t_N, R^t) \quad (2.5)$
```

subject to

```
$lambda^t < S^t, \rho F^t_i < C^t_i, i=1, \dots \mathcal{M}, \hat{A} \prod_{i=1}^{\mathcal{M}} \hat{D}_i < B^t, \hat{A} a^s + \mathbf{b} \hat{C}^i + \mathbf{b}^g \geq G \geq f z_{max}$
```

where: $\frac{T^{tot(t)}}{FCFS_{max}}$, given by Equation 2.2, is the mean service response time for all applications; $z_{max}$ is the upper bound of the resource cost.

The service response time minimization problem (Equation 2.5) is a convex optimization problem [34]. We apply the primal-dual interior-point methods [34] to solve the optimization problem (Equation 2.5).

+ 2. Resource cost minimization problem. Since applications have different requirements on service response time, multimedia service providers have to guarantee QoS provisioning for all applications. However, it is challenging to configure cloud resources to provide satisfactory services at the minimal resource cost. Thus, we formulate the resource cost minimization problem, which can be stated as: to minimize the total resource cost in the FCFS case by jointly optimizing the allocated scheduling resource, the computation resource, and the bandwidth resource, subject to the queuing stability constraint in each queuing system and the requirement on service response time for each application. The problem can be formulated as follows.

```
$M \in minimize \frac{T^{tot(t)}}{FCFS} (S^t_1, \dots, S^t_N, R^t) = \hat{A} a^s + \mathbf{b} \hat{C}^i + \mathbf{b}^g \geq G \quad (2.6)$
```

# Cloud Computing and Digital Media

subject to

$L^t < S^t$
$L_i^t F_i < C_i^t, i=1, \dots \rho \mathcal{M}$
$\hat{A}_{i=1}^{M} \lambda^t D_i < B^t$
$T_{FCFS}^{tot(i(t))} = t_i^t, i=1, \dots \rho \mathcal{M}$

where:
$T_{FCFS}^{tot(i(t))}$ is the service response time for class-$i$ application, which is given by Equation 2.3
$t_i^t$ is the upper bound of the service response time for class-$i$ application.

The resource cost minimization problem (Equation 2.6) is a convex optimization problem, which can be solved efficiently using the primal–dual interior-point methods [34].

### 2.3.2.2 Priority scheme Case

The FCFS scheme is not suitable for the multimedia applications that require differentiated services. For example, the urgent multimedia applications, such as the real-time health monitoring, need to be processed as soon as possible; thus, these requests should have a higher priority than the other requests. We extend our resource optimization to the priority service case, in which multiple applications with different priorities are provided. The requests for the higher priority applications should be ahead of those for the lower priority applications. Specifically, we study the preemptive priority queuing discipline, in which the requests with a higher priority obtain the service immediately even if other requests with a lower priority are being served, and preempted requests will later be resumed from the last preemption point.

Suppose that there $M$ classes of applications with different priorities, which are denoted as class-1, 2, ..., $M$, respectively. A smaller class number corresponds to a higher priority. The mean arrival rate of class-$j$ requests is denoted by $\lambda^t$. According to the composition property, the total request arrival follows the Poisson process with an average $\lambda^t = \hat{A}_{m=1}^M \lambda^t$. When requests arrive at the data center, the master server always schedules the request with

# Resource Optimization for Multimedia Cloud Computing ■ 35

the highest priority first. The lower priority requests can be scheduled only after all higher priority requests have left the schedule. Therefore, the scheduling queue is modeled as an M/M/1 queuing system with preemptive priority service. The response time for scheduling class-j requests is given by

```
$T_{prio}^{sch(j)(t)} = \frac{1/S^t}{1-s_{ach}^{j-1}} + \frac{\hat{A}^{\frac{j}}{k}/S^t}{(1-s_{ach}^{j-1})(1-s_{ach}^j)}$
```

where:
$s_{ach}^j = \hat{A}^j_{k-1} \lambda^t/S^t$

To make the scheduling queue stable, $s_{ach}^m = \hat{A}^m_{k-1} \lambda^t/S^t<1$ should be satisfied. In the computation phase, $M$ computation queues are used to store requests with the corresponding priority. The requests with the highest priority have preemptive right to obtain service immediately. The total computation resource is denoted by $C^t$, and the average task size of class-j is $F_j$. The service time for computing class-j requests is assumed to be exponentially distributed with mean time $F_j/C^t$. According to [30], the response time for processing class-j requests is given by

```
$T_{prio}^{com(j)(t)} = \frac{F_j/C^t}{1-s_{com}^{j-1}} + \frac{\hat{A}^{\frac{j}}{k}}F_j/C^t}{(1-s_{com}^{j-1})(1-s_{com}^j)}$
```

where:
$s_{com}^j = \hat{A}^j_{k-1} F_j/C^t$

Moreover, $s_{com}^m<1$ is required to maintain queue stability. Since the rates are different for different applications, the mean response time at computing server is given by

```
$T_{prio}^{com(t)} = \frac{\hat{A}^{\frac{m}}{k-1}}\frac{T_{prio}^{com(j)(t)}}{\lambda^t}$
```

After processing, all service results are sent to the transmission queue. The results in the higher priority classes are transmitted to those in the lower priority classes. The allocated bandwidth resource is denoted by $B^t$, and the average result size of class-$j$ application is denoted by $D_j$. Thus, the mean transmission time is given by $D_j/B^t$. The response time for transmitting class-j results is given by

```
$T_{prio}^{j(t)} = \frac{D_j/B^t}{1-s_{tra}^j} \cdot \frac{\hat{A} \mathbb{1}_{D_k/(B^t)}^{k=1}}{(1-s_{tra}^j)}$
```

where: $s_{tra}^j = \hat{A}_j^t \mathbb{1}_{D_k/B^t}$

To ensure the transmission queue is stable, $s_{tra}^j < 1$ should be satisfied. Thus, the mean response time at the transmission server can be formulated as

```
$T_{prio}^{tot(t)} = \hat{A} (\mathbb{1}_{T_{tra}^{j(t)}^{j-1}) T_{prio}^{j(t)}$
```

Based on the above derivations, the total response time in priority service is the summation of response time in the three phases, which can be given by

```
$T_{prio}^{tot(t)} = T_{prio}^{ach(t)} + T_{prio}^{com(t)} + T_{prio}^{tra(t)} \quad (2.7)$
```

Furthermore, we can get the service response time for the class-j application as follows:

```
$T_{prio}^{j(t)} = T_{prio}^{ach(j(t))} + T_{prio}^{com(j(t))} + T_{prio}^{tra(j(t))} \quad (2.8)$
```

The total resource cost in the priority service case is formulated as

```
$Z_{prio}^{tot} = (aS^t + bC^t + g\mathcal{G}^t) \quad (2.9)$
```

+ 1. Service response time minimization problem. In multimedia cloud, priority service discipline has been used in many applications. The applications with more stringent delay requirement should receive a higher priority service, whereas the less delay-sensitive multimedia applications can be served in a lower priority. The multimedia service providers have to support different priority services and minimize the mean response time. We formulate the service response time minimization problem in the priority service case, which can be stated as follows: minimize the mean service response time for all applications by jointly optimizing the allocated scheduling resource, the computation resource, and the bandwidth resource, subject to the queuing stability constraint in each queuing system and the resource cost constraint. Mathematically, the service response time minimization problem can be formulated as

```
$Minimize \quad T_{prio}^{(tot)}(S^t, F^t, B^t) \quad (2.10)$
```

subject to

```
$lambda^t < S^t\n\sum_{j=1}^{n} \hat{A}_{ij}^t F_j < C^t\n\sum_{j=1}^{n} \hat{A}_{ij}^t D_j < B^t$
```

```
$(S^t + bC^t + \mathcal{B}^t g \le z_{max})$
```

where:
$T_{prio}^{(tot)}$ is given in Equation 2.7
$z_{max}$ is the upper bound of the resource cost.

The service response time minimization problem (Equation 2.10) is a convex optimization problem, which can be efficiently solved by the primal–dual interior-point methods [34].

In the priority reactive case, the requests with the highest priority have the preemptive right to receive service. Therefore, the imposition of priorities decreases the mean delay of higher priority requests and increases the mean delay of lower priority requests. However, the effect of imposing priorities for the overall service response time of all requests is not determined. To address the issue of how the imposition of priorities affects the overall service response time, Schrage and Miller [35] propose the shortest processing time (SPT) rule, which is described as follows: (1) if the objective of a queue is to reduce the overall mean delay, a higher priority should
