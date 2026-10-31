
work across multiple agents. For example, while distributing work related to bank accounts across many agents, you might want to ensure that all the work related to a particular account executes in a single agent. One of the principal advantages is that since all work related to an instance occurs in the one agent, locking can be local and therefore more efficient. In general, this is the preferred approach for managing any stateful object, especially state machines.

TIBCO BusinessEvents provides a mechanism for realizing this type of load distribution: content-aware load balancing. This is a variation on the load balancing shown in Figure 14-8. The load-balancing configuration not only specifies the routing and worker inference agents, but also a property of the event to be used in directing the event to the workers. The load balancer ensures that all events with the same property value (e.g., the account number) are sent to the same worker.

You may encounter situations in which the incoming event does not contain the precise value you want to use to govern the distribution. In such cases you can specify a preprocessor function that computes the value and assigns it to a property of the event. Other than this type of preprocessor function, the Load Balancer IA has no business logic. The Worker IA agents execute all the logic needed to process the event.

## Managing Sequencing

Many applications present situations in which it is important to maintain the order in which things are done. If you are performing transactions on a bank account, for example, it is important that the deposits and withdrawals actually be executed in the same sequence in which they were initiated.

Sequencing becomes a challenge when there are multiple parties doing the work in parallel (Figure 14-9). Despite the fact that the source sends request 1 before request 2, in the absence of any coordination there is no guarantee that result 1 will be produced before result 2. So the question becomes how to preserve sequencing when taking advantage of parallel processing.

This question breaks down into two sub-questions: how to preserve sequencing within a single worker when the worker internally uses parallel processing, and how to preserve sequencing when there are multiple workers. These questions are addressed in Architecting Composite Applications and Services with TIBCO® when TIBCO ActiveMatrix® Service Grid components (including TIBCO ActiveMatrix BusinessWorks™) play the roles of the worker. Let's take a look at how these questions are addressed when an inference agent is the worker.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_230_0.png)

Figure 14-9: The Sequencing Problem

### Preserving Sequencing within One Inference Agent

By default, preprocessing in an inference agent uses a shared pool of threads. This default configuration is inherently parallel and cannot preserve sequencing. In order to preserve sequencing within the inference agent, two things are necessary.

1. Use a JMS queue (and corresponding JMS destination) for delivering requests. JMS guarantees that, between a single publisher and a single subscriber, messages will be delivered in the order sent.
2. In the configuration of the JMS destination in the CDD, select the Caller’s Thread threading model. For JMS destinations, there is a single thread handling input messages, and this choice selects that thread for doing both the preprocessing and the RTC cycle execution.

These choices, together, ensure that an inference agent will preserve sequencing while processing requests.

### Preserving Sequencing across Multiple Inference Agents

To ensure sequential processing, you need to use the content-aware load balancing described earlier in this chapter along with some additional configuration requirements.

- Use a JMS queue (and corresponding JMS destination) for delivering requests. JMS guarantees that, between a single publisher and a single subscriber, messages will be delivered in the order sent.
- Use an inference agent configured as a router. In the configuration of its JMS destination in the CDD, select the Caller’s Thread threading model. For JMS destinations, there is a single thread handling input messages, and this choice ensures that the preprocessing (which does the routing) will be single threaded.
- For each worker inference agent, in the configuration of its JMS destination in the CDD, select the Caller’s Thread threading model. For JMS destinations, there is a single thread handling input messages, and this choice selects that thread for doing both the preprocessing and the RTC cycle execution.

### Recovering Temporal Sequencing (Reordering)

This situation arises when you have events arriving at a destination out of sequence and you wish to restore the original sequence. Be aware that this is fundamentally a hard problem, one for which there is no generic solution.

The hardest part of this problem lies in knowing when you have received all of the relevant events. Even if you have one distinguished event that is supposed to be last in the sequence, if it arrives out of sequence you will not realize that there are other events still in the pipeline. You can’t even begin to address the problem unless you have a working approach for this.

If you are using timestamps in the events as the basis for establishing the sequencing, there is another challenge you may encounter: clock skew. This problem arises when the timestamps are generated by different machines. Keeping clocks synchronized on multiple machines is a notoriously difficult problem. The resulting error, known as clock skew, will produce errors in the timestamps which, in turn, will produce errors in the sequencing.

One common strategy is to not even attempt the sequence restoration; instead, throw away all but the most recent event. When using

## Summary

Information can be shared between agents either directly, using events, or indirectly using objects in the cache. If the cache is used, inference and process agents must explicitly retrieve the information from the cache. This retrieval must be triggered by an event and that event must contain sufficient information to identify the object(s) that must be retrieved.

When multiple agents are sharing information in the cache, locking must be used to ensure data integrity. Locks are logical: What is locked is an identifier that corresponds to the object being locked, typically the object’s extID. Local locks can be used if the design ensures that the object being locked can only be present in the local agent; otherwise, global locks must be used.

One mechanism for ensuring that objects are only present in a single agent is to distribute load in such a way that all the work involving a given object is always sent to the same agent. Content-aware load distribution can be used for this purpose.

In some situations it may be important to process events in the order in which they are received. Within an inference agent, this can be accomplished by using a JMS queue and the Caller’s Thread to process the event. This makes the agent single-threaded with respect to that queue. When multiple agents are involved, content-aware load distribution must also be employed.

The use of JMS queues can result in the duplicate delivery of events when agents are shut down unexpectedly. Duplicate delivery can be detected by adding a JMSRedelivery property to the event. If there are non-idempotent activities being performed, logic must be added in the event of redelivery to determine whether the activity was previously completed and to take appropriate alternate actions.

## Part IV: Deployment

## Chapter 15: Case Study: Nouveau Health Care

### Objectives

One of the challenges in writing about architecture and architecture patterns is to pick examples that are rich enough to motivate the discussion and realistic enough to represent real-world challenges while at the same time being simple enough to be readily explained.

The fictional Nouveau Health Care case study was created for this purpose. Its business processes, though simplified when compared with their real-world equivalent, are still complex enough to present most of the common design challenges found in their real-world counterparts. An important aspect of reality is that the processes and their corresponding solution implementations do not operate in isolation; rather, they interact with one another and with other business processes as they would in the real world.

Different aspects of the Nouveau Health Care example are used throughout this architecture book series. This chapter provides a conceptual overview of the company and its business processes, and then introduces the Claim Tracker and its related business processes, which are used to illustrate many of the points and design principles in this book.

After reading this chapter you will be able to describe the Claim Tracker requirements and architecture.
