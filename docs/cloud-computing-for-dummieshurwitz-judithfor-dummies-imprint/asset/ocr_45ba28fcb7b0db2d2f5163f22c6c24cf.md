A set of loosely coupled components does the same work that software components in tightly structured applications used to do, but with loose coupling you can combine and recombine the components in a bunch of ways. This makes a world of difference in the ability to make changes easily, accurately, and quickly. (See the next section for more information on loose coupling.)

SOA components are orchestrated to link through business processes to deliver a well-defined level of service. SOA creates a simple arrangement of components that, together, deliver a very complex business service. Simultaneously, SOA must provide acceptable service levels. To that end, the components ensure a dependable service level. Service level is tied directly to the best practices of conducting business, commonly referred to as business process management (BPM) — BPM focuses on effective design of business process and SOA allows IT to align with business processes.

# Loosening Up on Coupling

In traditional software architecture, various software components are often highly dependent on each other. These software component dependencies make the process of application change management time consuming and complex. A change made to one software component may impact lots of other dependent software components, and if you don’t make all the right changes, your application (or related applications) may fail. One small change to an application can make its way through the whole application, wreaking havoc and leading to massive software code revision.

Loose coupling makes it simpler to put software components together and pull them apart. Because they aren’t codependent, you can mix and match components with other component services as needed. This mix-and-match capability allows you to quickly create new and different applications from existing software services.

For example, if a credit card–checking service is loosely coupled from an ecommerce application and you need to change it, you simply replace the old one with the new one without touching any of the other applications that use the service.

An important aspect of loose coupling is that the component services and the plumbing (basic interaction instructions for the pieces) are separated so that the service itself has no code related to managing the computing environment. Because of this separation, components can come together and act as if they were a single, tightly coupled application.

![](bbox=[0.1, 0.66, 0.18, 0.76])