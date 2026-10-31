
TIBCO BusinessEvents can, of course, interact via its channels with any component using a supported transport. There are also additional integration capabilities in the product. This chapter explores these additional integration capabilities. After reading this chapter you will be able to describe how TIBCO BusinessEvents can interact with:

- TIBCO ActiveMatrix BusinessWorks™
- Web services
- Databases

## Interacting with TIBCO ActiveMatrix BusinessWorks™

TIBCO ActiveMatrix BusinessWorks™ has a plugin to simplify interactions with TIBCO BusinessEvents®. The use of the plugin enables ActiveMatrix BusinessWorks to define RuleServiceProvider Configurations. Each of these configurations contains pointers to the EAR and CDD files from a TIBCO BusinessEvents project with which you want to interact. The configuration also identifies a processing unit that is defined in the CDD file. When the ActiveMatrix BusinessWorks engine runs, it will run an instance of this processing unit in the same JVM as the ActiveMatrix BusinessWorks engine.³

³ A similar integration, in which an instance of TIBCO ActiveMatrix BusinessWorks executed in the same JVM as a processing unit, has been deprecated as of the 5.x release of TIBCO BusinessEvents.

The plugin provides four activities that can be employed in ActiveMatrix BusinessWorks processes: (1) Send Event, (2) Receive Event, (3) Wait for Event, and (4) Invoke RuleFunction.

### TIBCO ActiveMatrix BusinessWorks™ Send Event

The Send Event activity enables ActiveMatrix BusinessWorks to send an event to a specific destination in a processing unit (Figure 12-1). The configuration of this activity shows the event data structure so that values can be readily mapped to the event properties. Executing the activity sends the event to the specified destination.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_199_0.png)

**Figure 12-1:** *TIBCO ActiveMatrix BusinessWorks™ Sending an Event*

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_199_1.png)

**Figure 12-2:** *TIBCO ActiveMatrix BusinessWorks™ Waiting for an Event*

### TIBCO ActiveMatrix BusinessWorks™ Wait for Event

The Wait for Event activity is a blocking activity in an ActiveMatrix BusinessWorks process (Figure 12-2). When the process executes the activity, it waits for TIBCO BusinessEvents to send the event. The properties of the event are available to the ActiveMatrix BusinessWorks process.

The Wait for Event activity can be used in conjunction with the Send Event activity to implement a synchronous request-reply interaction between ActiveMatrix BusinessWorks and TIBCO BusinessEvents.

### TIBCO ActiveMatrix BusinessWorks™ Receive Event

The TIBCO ActiveMatrix BusinessWorks Receive Event activity is an ActiveMatrix BusinessWorks process starter (Figure 12-3). When TIBCO BusinessEvents sends an event of the indicated type, the ActiveMatrix BusinessWorks process starter receives the event and creates an instance of the process that uses that event as its process starter. The properties of the event are available for use in the process.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_201_0.png)

(a) Synchronous Interaction

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_201_1.png)

(b) Asynchronous Interaction

Figure 12-5: TIBCO BusinessEvents® as a Service Provider

socket connections. Commonly an inference agent is used as the service provider, but process agents and even query agents can play this role as well.

In most situations, when the agent is playing the role of a service provider, the receipt of the request is the triggering event for all of the processing required to produce the result. After receipt of the request, processing continues until the result is produced.

In some situations, when the agent plays the role of an asynchronous provider, the receipt of the request does not trigger all of the work: Some remainder of the work is performed in response to another event. In some situations this event is directly related to the request—a timer expiring or an asynchronous response from some back-end system. In other situations, the other event may be an update to a cached concept whose change triggers the generation of the response (see Reference-Data Change Coordination pattern in Chapter 10).

## TIBCO BusinessEvents® as an Asynchronous Service Consumer

Consuming services with an asynchronous interaction is fairly straightforward with TIBCO BusinessEvents. However, asynchronous interactions generally require the retention of contextual information required to process the response. There are three design patterns that can be used for maintaining this context:

- Concept Maintains Asynchronous Context
- State Machine Maintains Asynchronous Context
- Process Maintains Asynchronous Context

### Concept Maintains Asynchronous Context

With this approach an inference agent sends the Request in the action part of a rule or in a preprocessor function (Figure 12-6). A concept is also created or updated with any contextual information needed to process the reply.

When the Reply is returned, the preprocessor function for the reply event retrieves the concept from the cache (assuming cache-only mode was used). To make retrieval possible, the identifier for the concept (typically the extID) must be included in the request and returned in the reply. The service provider must also be designed to return the identifier from the request in the reply. If JMS is used for the transport and the extID of the concept is used as the JMSCorrelationID of the request, the JMS specification requires that the service provider pass this same value back as the JMSCorrelationID of the reply. The reply is then processed either in the preprocessor function or in rules triggered by the arrival of the reply event.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_202_0.png)

Figure 12-6: Concept Maintains Asynchronous Context

In sending the Request, if the concept that will hold the context already exists, the Request must be sent in the action part of the rule since a preprocessor function cannot modify an existing concept—it can only create a new concept.

### State Machine Maintains Asynchronous State

The TIBCO BusinessEvents® Data Modeling extension adds state machine capabilities to concepts. This makes possible a pattern that uses a state machine to maintain the asynchronous state and also to manage the entire interaction. A sketch of such a state machine is shown in Figure 12-7.

Recall that a state machine is owned by a concept (Chapter 5). When the state machine starts, the Request it sends contains a data element, the extID of the concept owning the state machine. This extID is expected to be returned in the Reply and will be used to correlate the reply with this particular state machine instance. The state machine then enters a state where it is waiting for a reply. When a reply arrives with a matching extID, the machine makes another transition.

As for actions to be taken when the reply is received, there are two possible approaches. One is that the actions can be part of the state machine structure, executed when state transitions are taken or when states are entered or exited. The other approach is to place actions in the action part of a rule that is triggered when a change occurs to the state machine. From a rule perspective, this is a change to the concept that owns the state machine.

One advantage of this approach is that the state machine has timer infrastructure that can be used to recognize that a reply has not been received within a designated period of time.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_203_0.png)

Figure 12-7: State Machine Maintains Asynchronous State

## HTTP Send Request Invocation

This pattern uses the catalog HTTP function sendRequest(). It can be used for both conventional HTTP request-reply interactions and for SOAP interactions (Figure 12-9). Care should be exercised when using this pattern, as the thread making the call is tied up while waiting for the reply. When there are many threads available, such as when executing a preprocessor function, the blocked thread may be only a condition to be considered when deciding the size of the thread pool. However, when the function is executed in the action part of a rule and the RTC is configured to be single threaded, all RTC processing will be blocked until the request completes.

## TIBCO BusinessEvents® Process Orchestration

### Web Service Invocation

The TIBCO BusinessEvents Process Orchestration extension includes a Web Service task, which is used for synchronous service invocations (Figure 12-10). Recall that all tasks are executed by a pool of threads in

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_205_0.png)

Figure 12-9: HTTP Send Request Invocation

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_205_1.png)

Figure 12-10: TIBCO BusinessEvents® Process Orchestration Web Service Invocation
