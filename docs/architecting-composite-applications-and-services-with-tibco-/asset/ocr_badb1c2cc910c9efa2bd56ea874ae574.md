# Composite Service Architecture

In a composite, two or more components (or services) collaborate to collectively provide the required functionality. A composite may be an entire solution, a fragment of a solution, or the internal structure of one of the solution components or services. Most solutions are composites.

Services are often implemented as composites, particularly when the service serves as a wrapper around existing functionality implemented in another component. Ideally you would like to treat the service (or any component) as a black box whose internal details can be ignored. However, the black-box approach is not always appropriate, as will be discussed in Chapter 5. For now, we’ll simply examine the architecture of a composite service and ignore the question as to what portion of that architecture properly belongs in the service specification architecture (because it is observable) as opposed to the service implementation architecture (because it is not).

# Composite Service Architecture Pattern

Let’s suppose that the Account Manager is actually a façade wrapped around a Legacy Accounting System (Figure 1-18). It is important for

![](bbox=[0.35, 0.7, 0.7, 0.92])

Figure 1-18: Composite Service Architecture Pattern