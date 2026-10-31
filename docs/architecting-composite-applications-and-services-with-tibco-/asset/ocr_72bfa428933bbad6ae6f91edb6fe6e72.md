![](bbox=[0.38, 0.17, 0.78, 0.56])

Figure 10-20: Dual Coordination-Pattern Processing

In the case of an asynchronous interaction, the service eventually performs the work and returns the result using a second asynchronous interface. To make life simple, it is a good idea to use exactly the same data structure definition for both the synchronous and asynchronous response. Thus only one data structure definition is needed and the same service consumer logic can be used to process both synchronous and asynchronous responses. The payClaim() operation of the Claim Payment Interface in the Nouveau Health Care example uses this design pattern.

# Summary

When approaching an SOA-based solution architecture, there are a number of questions facing the project architect. When there are multiple front-end systems to be supported, can they be supported by a single operation or are separate operations required? When back-end systems need to be accessed, should they be accessed directly, or should those interfaces themselves be wrapped in a service? Should the service contain all of the logic, or should it be factored into several services and combined in a composite service? Finally, what logic properly belongs in front- and back-end systems as opposed to the service(s) in