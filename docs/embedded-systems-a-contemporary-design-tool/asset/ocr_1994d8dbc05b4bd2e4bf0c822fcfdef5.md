light of some kind if that might help. He proposes to develop a remote-controlled two-color (Red and Green) light such as that shown in Figure P13.3.

![](bbox=[0.26, 0.14, 0.33, 0.24])

# Figure P13.3

(a) Devise an algorithm that will prevent two SUGs or a SUG and an FSG from entering the canal at the same time. Explain in detail how your design works and how it will solve the problem. Be certain to identify the minimum number of lights you will need and where they will be placed.

(b) What features/capabilities are you going to ask Vito to put into the light/remote control system?

(c) Does your solution require any equipment other than your buddy's light? If so, what might that be?

13.7 Consider the traffic deadlock shown in Figure P13.4.

![](bbox=[0.15, 0.46, 0.43, 0.66])

# Figure P13.4

(a) For the system, what are the resources and what are the processes?

(b) Draw a resource allocation graph capturing the processes and resources.

(c) Does the graph contain a cycle?

(d) Show that the four necessary conditions for deadlock hold. Be precise.

(e) Give a simple rule that will avoid deadlocks in the system.

(f) Show how or why your scheme will avoid deadlocks.

13.8 We have an embedded system with four tasks, T0-T3, and three resources, R0-R2. The system has nine instances of R0, three instances of R1, and six instances of R2. After the system has been running for a while, we have the state shown in Figure P13.5.

| Task | R0 Reqd. | R0 Alloc. | R1 Reqd. | R1 Alloc. | R2 Reqd. | R2 Alloc. |
|---|---|---|---|---|---|---|
| T0 | 3 | 1 | 2 | 0 | 2 | 0 |
| T1 | 6 | 5 | 1 | 1 | 1 | 1 |
| T2 | 3 | 2 | 1 | 1 | 4 | 1 |
| T3 | 4 | 0 | 2 | 0 | 2 | 2 |

# Figure P13.5

(a) If task T1 requests and is allocated one additional instance of resources R2, and R2, will this lead to a safe state?

(b) If so, what is the proper sequence of task execution that will ensure no deadlock?

(c) Propose a resource request and allocation from the above state that would not lead to a safe state.