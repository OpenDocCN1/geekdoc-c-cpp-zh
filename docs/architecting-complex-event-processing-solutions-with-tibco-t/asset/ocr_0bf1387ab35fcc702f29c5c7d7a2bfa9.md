the consuming agent is an inference or process agent. The consuming agent is not automatically aware of the cached information: It must explicitly load the concept from the cache. This requires that there be sufficient information in the event triggering the activity in this agent to identify the concept(s) that need to be loaded. This pattern also characterizes the behavior when the consuming agent is a query agent executing a snapshot query.

One potential problem with this pattern arises if the producing agent makes subsequent changes to the concept while the consuming agent is in the process of using the concept. This problem gives rise to the need for locking, which is described later in this chapter.

The pattern is a bit different when the consuming agent is a query agent running a continuous query or a dashboard agent (Figure 14-3). In this situation, the consuming agent is automatically notified when the cached object changes. In the case of the query agent, the object may be a cached event or a concept. In the case of a dashboard agent, the object is a metric. Locking is generally not an issue with this pattern.

A variant on these patterns arises when there are multiple agents that can modify the same concept (Figure 14-4). Here locking is clearly needed to maintain the consistency of the information residing in the concept.

![](bbox=[0.1, 0.7, 0.92, 0.82])

Figure 14-3: Information Sharing with a Continuous Query or Dashboard Agent via Cache

![](bbox=[0.18, 0.9, 0.8, 0.97])

Figure 14-4: Multiple Producers