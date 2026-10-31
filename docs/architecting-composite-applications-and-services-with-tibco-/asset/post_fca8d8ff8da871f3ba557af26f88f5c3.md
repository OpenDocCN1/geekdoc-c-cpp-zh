
references a particular version of the service specification for details rather than replicating that information.

## Nonfunctional Requirements

### Performance

For each of the interface operations, the contract specifies the peak rate at which the operation will be invoked and the response time that has been agreed to. This information provides the basis for capacity planning for the service provider.

### Availability

For each of the interface operations, the contract specifies the agreed-to availability and maximum outage time.

### Site Disaster Recovery

If site disaster recovery is supported for the service, for each of the interface operations, the contract specifies the agreed-to recovery point objective and recovery time objective in the event of a site disaster recovery.

### Security

If security is to be enforced, the details specific to the service consumer are detailed.

### Deployment

For each of the environments covered by the contract, it specifies the location of the service provider and consumer, the interface transport specifics, and the endpoint details.

## Service Architecture

There are a number of parties that must be aware of the internal architecture of the service provider. The organizations responsible for the deployment, operation, and support of the service need to understand how it works. Solution architects need to understand enough about the architecture to be able to understand its limitations and behavior under unusual circumstances. This is particularly important when the architects are evaluating the feasibility of expanding the service's usage beyond the bounds of its present specification. Even the service consumers may need to be at least partially aware of the architecture when load distribution and fault tolerance expose sub-components of the architecture.

The service architecture is documented much as you would any architecture, with emphasis on process models, the architecture pattern of the service, and the process-pattern mapping. In the case of the service, the processes are the intended utilization scenarios and the mappings indicate how those scenarios are executed by the components of the architecture pattern.

### Payment Manager Architecture Pattern

The architecture pattern for the Payment Manager is shown in Figure 6-14. At the top level, the payment manager consists of two components: the Payment Manager Composite (an ActiveMatrix composite) and a Database playing the role of an operational data store (ODS).

The composite contains three ActiveMatrix BusinessWorks components: the Claim Payment BW Service, the Settle Deferred Payments BW Process, and the Settlement BW Service. The Claim Payment BW Service implements the Claim Payment Interface and has a BusinessWorks sub-process for each of the service operations. The Settle Deferred Payments BW Process is triggered on a timer and settles deferred payments. The actual mechanics of settlement are abstracted into the Settlement BW Process since they are used in two places: the Pay Claim BW Process in the event of an immediate payment and Settle Deferred Payments BW Process in the event of a deferred payment. Note that the references made by the Get Pending Settlements BW Process, Get Provider Settlements BW Process, and Cancel Pending Payments BW Process have yet to be defined.

### Payment Manager Behavior Implementations

The behaviors that the payment manager exhibits are the triggered behaviors of the service specification.

### Payment Manager Behaviors

### Immediate Payment Behavior

The design for the Immediate Payment Behavior is shown in Figure 6-15.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_183_0.png)

### Figure 6-15: Immediate Payment Behavior

![](img/b8d8132a583ad73d511c4c1bb92e2df7_184_0.png)

Coordination Legend synchronous interaction asynchronous interaction delegation interaction

### Figure 6-16: Deferred Payment Behavior

![](img/b8d8132a583ad73d511c4c1bb92e2df7_185_0.png)

### Figure 6-17: Settle Deferred Payments Behavior

## Summary

A variety of different documents are required to support the effective development and use of services. Some are simple, such as the one-line description and abstract, which are designed to aid a potential service consumer in identifying services of potential interest. The service specification provides a detailed definition of the service from the perspective of a service consumer. In addition to being the source of the one-line description and abstract, the specification describes:

- The intended service utilization scenarios
- The service interfaces
- The components and interfaces on which it depends
- The observable state of the service
- The behavior resulting from each triggering event
- How service activity is coordinated with that of external components
- The constraints on the use of the service operations
- The nonfunctional capabilities of the service
- Deployment specifics of which the service consumer must be aware

The service specification describes the overall capabilities of the service but does not indicate how those capabilities are allocated to different service consumers. That is the purpose of a service usage contract. Each contract specifies the support that the service will provide for a specific service consumer. It covers

- The relationship between the organization(s) responsible for the service provider and those responsible for the service consumer
- The scope of the service consumers covered by the contract and the mechanisms to be used to access the service
- The specific functional capabilities of the service that will be provided to the service consumer (generally a subset of the overall service capabilities)
- The nonfunctional requirements to be met for this consumer, particularly with respect to performance, availability, and security
- Deployment specifics, such as the access points in the various environments

The service architecture is also of interest to some parties, particularly solution architects who need to evaluate the feasibility of pushing the service beyond its present specification in terms of breakdown detection, performance, availability, and site disaster recovery.

## Chapter 7

## Versioning

### Objectives

Despite your best efforts to conceptualize services so that they can be used without modification, at some point it is inevitable that one will have to be changed. Such changes impact not only the interface definition, but the providers and consumers of the service as well. This makes it necessary to identify the versions of each and track the dependencies between them.

Nowhere is this issue more prominent than in the Open Services Gateway initiative framework (OSGi Framework¹). This framework provides a standardized approach to defining and integrating components. Significantly, it makes it possible to avoid conflict while incorporating multiple versions of interfaces, service consumers, and service providers.

The OSGi Framework is of interest for two reasons. One is that the deployment model for the ActiveMatrix Service Bus node is based upon the framework. The other is that the best practices for managing versions in the framework, as presented in the OSGi Alliance’s Semantic Versioning Technical Whitepaper², are generally applicable best practices for managing versions.

1. www.osgi.org/About/Technology#Framework

2. OSGi Alliance, Semantic Versioning Technical Whitepaper, Version 1.0 (May 6, 2010).

This chapter explores the issues raised when versioning services and presents best practices for dealing with these issues. After reading this chapter you should be able to describe the OSGi Alliance’s semantic versioning model and the best practices for service versioning.

### Dependencies and Compatibility

In a component- or service-based architecture, the interface is the point of contact between the consumer and provider of functionality (Figure 7-1). Both consumer and provider are dependent upon the interface, but in different ways.

The provider must implement all aspects of the interface. Consequently, any change to the interface mandates a change to the provider. Consumers, on the other hand, may only use a portion of the interface. A change to a consumer is only required when the used portion of the interface changes. In particular, additions to the interface do not require any changes to the consumer.

Interface changes that do not require changes to consumers are considered to be *backwards compatible*. Any other change is considered to be *incompatible*.

### Packages

In the OSGi Framework, the unit of assembly is a package containing interfaces, consumers, and providers. The package determines which of these are visible outside the package. Packages bring some complexity to representing version dependencies, as the following example illustrates.

Consider the Event Admin and Event Listener interfaces from the `OSGi.org.osgi.service.eventadmin` package shown in Figure 7-2. When an Event Destination wants to be notified of events, it provides an instance of the Event Listener interface and then registers that

![](img/b8d8132a583ad73d511c4c1bb92e2df7_188_0.png)

Figure 7-1: Versioned Elements and Their Dependencies
