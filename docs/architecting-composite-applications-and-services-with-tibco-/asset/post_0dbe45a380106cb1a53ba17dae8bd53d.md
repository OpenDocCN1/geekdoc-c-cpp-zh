
## Figure 13-6: Settle Deferred Payments Process Mapping

> This is an Out-Only interaction—requires a JMS queue.

Coordination Legend
asynchronous interaction
asynchronous interaction
delegation interaction

![](img/b8d8132a583ad73d511c4c1bb92e2df7_337_0.png)

![](img/b8d8132a583ad73d511c4c1bb92e2df7_338_0.png)

Coordination Legend
asynchronous interaction
asynchronous interaction
delegation interaction

Figure 13-7: Immediate Payment Composite Mapping

## Completing the Component Specifications

Once the architecture of the composite has been defined, the specifications for the individual components need to be defined. If any of the components are intended to be reusable services, then a separate specification document must be created for each of these. For non-reusable components, their specification information can simply be included in the architecture document for the composite. Note that the same set of information is required in either case.

## The Process of Architecting a Composite

The process of architecting a composite tends to be somewhat iterative in nature. It begins by defining a trial set of components, defining the composite architecture pattern, and selecting a behavioral management style. Then, one by one, the triggered behavior (from the composite specification) is mapped onto the components. The process of doing the mapping will lead to refinements in the components and the architecture pattern.

Once all of the processes have been mapped (be sure to map the exception scenarios), the individual component specifications can be completed.

## Composite Services and Applications

The term composite service has two similar but distinct meanings, both of which are valid. In one, the service itself is a composite of components as discussed earlier in the chapter. In the other, the service utilizes other services that are not components of the “composite service.” The distinction becomes apparent when you look at the specification for the service. When the underlying services are, themselves, part of the composite service, they do not appear in the service specification: They are part of the service architecture. When the underlying services are independent, then they appear in the service specification as part of the service context: Their interfaces appear as referenced interfaces, and the triggered behavior mappings show their participation in the behavior of the composite service.

A composite application is an application comprising multiple components. In other words, it is a distributed application. The performance of application work requires the coordinated participation of its constituent components.

The distinction between a composite application and a composite service is primarily one of intended use. A composite service provides functionality that is intended to be invoked by other system components in order to become part of an application or business process. Composite applications, on the other hand, provide usable functionality for users. This functionality might be in the form of a tool (e.g., an analytics engine such as TIBCO Spotfire®) or it might be an entire business process.

## Information Retrieval Design Patterns

Some composite services gather information from multiple sources and return it to the service consumer. There are two design patterns that can be used for this purpose: Cascading Control and Cached Information.

## Cascading Control Pattern

In the Cascading Control Pattern, when the composite service is invoked it turns around and makes calls on the underlying services to retrieve the required information (Figure 13-8). This is probably the first pattern that comes to mind when you are conceptualizing a composite service. But be aware of the performance implications. Every invocation of the composite service requires invocations of the underlying services, and the composite’s response time depends on the performance of the underlying services.

## Cached Information Pattern

An alternative to the Cascading Control Pattern is the Cached Information Pattern (Figure 13-9). In this pattern, rather than having the composite service retrieve information from its underlying services, the underlying services instead notify the composite when information request-reply interfaces (typically synchronous), while for cached information they present notification interfaces. The choice of pattern impacts the interface design of the underlying services.

The Cached Information Pattern is used by fedex.com for package status reporting. Underlying systems, which are responsible for managing the progression of packages from origin to destination, publish notifications of package status changes. A composite service at fedex.com, using the Cached Information Pattern, subscribes to those notifications and caches the package status information. When a customer goes to fedex.com and wants to know the status of a package, the composite service uses a local lookup from its cache rather than an interaction with a back-end system to provide the package status.

## Lookup and Cross Reference

A common type of information retrieval is a lookup: A piece of data is used as a key for looking up a corresponding piece of information. You might use a currency to look up the current exchange rate, or use the identifier of an entity in one system to locate the corresponding identifier for the same entity in a different system.

Frequent lookups can lead to performance problems, particularly if the information resides on disk. The use of a memory-resident cache can considerably speed up this process. TIBCO BusinessWorks™ SmartMapper provides the ability to cache data either in the ActiveMatrix BusinessWorks instance or in a separate process that is readily accessible by multiple BusinessWorks instances. Lookups are performed by BusinessWorks activities that are placed in the BusinessWorks processes that require the data. The cache is kept up to date by actively monitoring the underlying reference information and updating the cache when it changes. BusinessWorks™ SmartMapper also provides BusinessWorks activities that can create and manage the cross-reference information.

ActiveSpaces™ is also well suited for this task. The TIBCO ActiveMatrix BusinessWorks™ Plug-in for ActiveSpaces Software makes it easy to use the ActiveSpaces capabilities in a BusinessWorks process.

## TIBCO ActiveMatrix Composite Implementation

## Defining the Composite

Figure 13-10 shows the Payment Manager composite represented in SCA notation. Creating this representation in TIBCO Business Studio is the first step toward implementing the composite in the TIBCO ActiveMatrix platform.

## Selecting Implementation Types

The next step is to choose the implementation type for each component (Figure 13-11). In this case, ActiveMatrix BusinessWorks is selected for each of the three service implementations and a Mediation implementation type for the Notification Router.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_343_0.png)

Figure 13-10: SCA Representation of the Payment Manager Composite

![](img/b8d8132a583ad73d511c4c1bb92e2df7_344_0.png)

**Figure 13-11:** *Payment Manager Composite Showing Implementation Types*

## Summary

A composite is a collection of components wired together for some purpose. The specification for the composite indicates the externally observable structure and behavior of the composite, while its architecture defines how that structure and behavior are actually provided.

Architecting a composite is very much like architecting any other component. You determine the components you want as part of their interfaces and define the architecture pattern describing how they are

This page intentionally left blank

## Part IV

### Advanced Topics

This page intentionally left blank
