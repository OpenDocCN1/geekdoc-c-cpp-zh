We compare the different kinds of cohesion and coupling from several different perspectives in Table 9.1. The ranking is Excellent/Easy = 5 ... Poor/Difficult = 1.

# Table 9.1 Comparison of Coupling and Types of Cohesion from Different Perspectives.

| Cohesion | Coupling | Ease of modification | Ease of understanding | Ease of maintenance |
|---|---|---|---|---|
| Functional | 5 | 5 | 5 | 5 |
| Sequential | 4 | 4 | 4 | 3–4 |
| Communicational | 3 | 3 | 3 | 3 |
| Procedural | 2–3 | 2–3 | 2–3 | 2 |
| Temporal | 1 | 3 | 3 | 2 |
| Logical | 1 | 1 | 2 | 1 |
| Coincidental | 1 | 1 | 1 | 1 |

Cohesion and coupling analyses provide a good set of metrics by which to begin to assess the high-level architectural aspects of a design. Remember, however, that both are guidelines. The work to ensure that the design is solid and that it is thoroughly tested still needs to be done.

There are plenty of good designs that require tightly coupled modules; CDMA cell phones are a good example. One can have tightly coupled multiprocessor designs as well as designs based on message passing. The implication is not that one design is right or wrong, or better than the other; it is just how it was done to meet the requirements.

# 9.16.4 A Few More Considerations

**spatial** With today's systems, a spatial point of view is often essential. This is an external view of the system and it yields a distributed functional architecture. With such a view, performance and communication costs are taken into consideration. Closely associated with the spatial viewpoint is that of resource allocation; again, this is an external view. Such efforts result in a “resource architecture.” Once again, performance, costs, and dependability are factors that must be considered.

**hardware** Finally, one must consider the hardware and the software. Decomposition becomes a design process that leads to a hardware architecture as was discussed earlier. Now performance must be considered. As embedded developers, we are playing a direct role in the design and selection of the hardware platform as well as the software environment. Making trade-offs intelligently in these two areas can take us a long way toward developing a safe, robust, and high-quality/high-performance system.

# 9.16.5 Approaches to Partitioning and Mapping

As we take this next step in the design process flow, our objective is to allocate operations comprising system behavior to the hardware and/or the software. There are a variety of different methods by which to attack the partitioning problem. We recognize that there are two extremes: a software-oriented model and a hardware-oriented model. The former