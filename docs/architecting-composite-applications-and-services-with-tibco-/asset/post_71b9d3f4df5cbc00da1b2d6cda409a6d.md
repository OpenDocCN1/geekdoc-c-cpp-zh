
![](img/b8d8132a583ad73d511c4c1bb92e2df7_384_0.png)

## Figure 15-3: Default JMS Thread Usage

from the JMS Binding thread pool, which is a subset of the JCA thread pool. There is at present no mechanism for designating a different thread pool. Thread ② executes the SOAP binding logic, the service virtualization required to interact with the component, the component logic, and ultimately places the response message on the response queue. This pattern describes the thread usage for both Java and Mediation implementation types.

If the Java component makes an outbound SOAP/HTTP call, thread ② will execute the outbound HTTP call as was shown in Figure 15-2. Figure 15-4 shows the default thread usage for outbound JMS communications. By default, the component’s worker thread ④ places the outbound message on the JMS queue. This thread is then released. A JMS client/session thread (not from one of the pools) ③ listens for responses on the reply queue. When a response arrives, another worker
thread ① is obtained from the JMS Binding’s thread pool. Thread ④ then resumes execution, ultimately placing the response to the original client on the reply queue.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_385_0.png)

Figure 15-4: Default JMS Thread Usage for Outbound JMS Communications

## Default Node-to-Node Communications Thread Usage

When a service and its implementing component are deployed on different nodes, the messaging bus is used for communications between the nodes. Figure 15-5 shows the thread utilization for an inbound HTTP call. On Node 1, the worker thread ② publishes the request to the JMS queue and blocks, waiting for the reply. On Node 2, the JMS client/session thread ③ picks up the message and gives it to a virtualization worker thread ④ from Node 2’s virtualization thread pool. That thread executes the Java or Mediation logic and places the reply message on the response queue. Back on Node 1, the JMS client/session thread ⑤ picks up the message and gives it to a worker thread ⑥ from

![](img/b8d8132a583ad73d511c4c1bb92e2df7_387_0.png)

response comes back, the JMS client/session thread ⑤ obtains a new worker thread ⑥ from the virtualization thread pool. This worker thread then completes the process of placing the client’s response on the response queue.

## Thread Usage with the Virtualize Policy Set

The virtualize policy set makes wired elements communicate as if they were on different nodes. When a Virtualize Policy Set is applied to any of the wired services or references (or to the composite as a whole,
which applies it to all services and references in the composite), the communications between the wired elements will occur using the messaging bus. The resulting thread usage for an HTTP initiation is shown in Figure 15-7. Note that the thread usage is identical to that shown in Figure 15-5, except that here all the elements are deployed on the same node. This is, in fact, the intent of this policy: to make the interactions occur as if the components were deployed on separate nodes.

The thread utilization for a virtualize policy set and JMS initiation is shown in Figure 15-8. Again, note the similarity with Figure 15-6.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_388_0.png)

**Figure 15-7:** *Thread Usage with the Virtualize Policy Set and HTTP Initiation*

![](img/b8d8132a583ad73d511c4c1bb92e2df7_389_0.png)

Figure 15-8: Thread Usage with the Virtualization Policy Set and JMS Initiation

## Thread Usage with the Threading Policy Set

Any service or reference can have a threading policy set associated with it. Figure 15-9 shows the thread utilization when the threading policy set is associated with either a promoted service with an HTTP binding or with the component service to which it is wired. The HTTP Connector worker thread ① hands off control to a worker thread ② from the pool specified by the threading policy. The HTTP Connector

![](img/b8d8132a583ad73d511c4c1bb92e2df7_391_0.png)

## Figure 15-10: Use of Policy-Specified Pool Threads with JMS Worker Threads

blocks, waiting for the response. When the response is received, it is handed back to the HTTP worker thread ② which completes the component work and hands the ultimate response back to the SOAP client.

Figure 15-12 shows the use of policy-specified threads in a reference when the initial thread is a JMS worker thread. The JMS worker thread ① hands off to a thread ② from the policy-specified pool and is then released. Thread ② places the request on the outbound JMS queue and then it, too, releases. When the response comes back, a JMS client/session thread ④ obtains a thread ③ from the policy-specified thread pool and passes the message to it. This thread then completes the processing, ultimately placing the client’s response message on the JMS queue.

## ActiveMatrix BusinessWorks™ Service Engine Architecture

## Thread Pools

ActiveMatrix BusinessWorks has three thread pools of interest:

- 1. Engine thread pool
- 2. Zero or one Tomcat thread pool
- 3. Zero or one HTTP Component thread pool

The ActiveMatrix BusinessWorks Service Engine has an additional thread pool:

- Invoke Partner thread pool

## Engine Thread Pool

The engine thread pool threads actually execute the ActiveMatrix BusinessWorks process definitions. The number of worker threads is established by the Engine.ThreadCount property on the ActiveMatrix BusinessWorks Service Engine instance.

## Setting the ActiveMatrix BusinessWorks Service Engine HTTP Server Type

Although ActiveMatrix BusinessWorks can use the Service palette to provide services that are accessible in SCA composites, it can also directly provide service interfaces. HTTP service interfaces provided in this manner require an HTTP server configuration. BusinessWorks provides two HTTP server options: Tomcat and HTTPComponent. These are the allowed values of the bw.plugin.http.server.serverType property on the ActiveMatrix BusinessWorks Service Engine instance.

## Tomcat Thread Pool

If Tomcat is selected as the HTTP server, two parameters are used for its configuration:

- 1. bw.plugin.http.server.minProcessors: This establishes the minimum number of HTTP server threads.
- 2. bw.plugin.http.server.maxProcessors: This establishes the maximum number of HTTP server threads.

## HTTPComponent Thread Pool

If HTTPComponent is selected as the HTTP server, one parameter is used for its configuration:

- `bw.plugin.http.server.httpcomponents.workerThread`: This establishes the number of HTTP server worker threads.

## Invoke Partner Thread Pool

The Partner definitions in ActiveMatrix BusinessWorks processes correspond to the references on the ActiveMatrix BusinessWorks Service Engine components in ActiveMatrix composites. Partner invocations use threads from the Invoke Partner thread pool. The number of threads in this pool is configured by the `InvokePartnerServiceActivityThreadPool.ThreadCount` property on the ActiveMatrix BusinessWorks Service Engine instance.

## ActiveMatrix BusinessWorks Internal Architecture

The internal engine architecture of ActiveMatrix BusinessWorks is shown in Figure 15-13. Processes in BusinessWorks, called Jobs, are represented by data structures. These data structures represent the entire state of the job, including all data associated with the job.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_394_0.png)

**Figure 15-13:** *ActiveMatrix BusinessWorks Internal Architecture*

## Process Starters

Process starters create the job data structures and place them in the Job Pool in memory or page them to disk (see the section on Max Jobs). There are various types of process starters, differing in the sources of the events that start the jobs. Process starters include

- Adapter Subscribers (events from TIBCO Adapters)
- File Poller (recognizes file system changes)
- On Event Timeout (exception handling when a WaitFor activity times out)
- On Notification Timeout (exception handling for a Notify activity)
- On Shutdown (process to execute when the engine shuts down)
- On Startup (process to execute when the engine starts)
- Timer (starts process at a specific time or periodically)
- HTTP Receiver (receipt of an HTTP input)
- JMS Queue Receiver (receipt of a message from a JMS queue)
- JMS Topic Receiver (receipt of a message from a JMS topic)
- Receive Mail (receipt of an e-mail message)
- Rendezvous Subscriber (receipt of a Rendezvous message)
- RMI Server (receipt of an RMI request)
- Service shared configuration (associated with a WSDL portType, acts as a process starter for a collection of processes, each associated with a different WSDL operation of the portType)
- SOAP Event Source (receipt of a SOAP request)
- TCP Receiver (client requests a TCP connection—the process manages the subsequent dialog)

For most of the process starters, a thread is dedicated to each defined process starter in the deployed project. This thread listens for the event and creates the job data structure. The exceptions are the process starters involving HTTP and JMS.

Process starters using HTTP Connections have multiple threads. These threads are taken from either the Tomcat or HTTPComponent thread pools discussed earlier. Each process starter references an HTTP Connection that specifies the configuration to be used. Note that while the job is actually executed in an engine thread, the HTTP threads block until the job returns the required HTTP response.

JMS interactions are described in the following section.
