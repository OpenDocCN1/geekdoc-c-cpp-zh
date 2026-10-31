# How Is SOA Different?

While current distributed systems development practices design layers and deploy them in physical tiers, SOA unifies these two concepts into "services," which are both the unit of design and deployment. The other aspect that differentiates SOA from current practice is the codification of communication between services; while there are no restrictions on how layers or tiers should communicate, services must communicate according to message-exchange-patterns defined by a schema. There is also both theoretical and practical support for using only one-way asynchronous messaging for inter-service communication; however, this has not yet won industry-wide support.

# Note

Note that "schema" doesn't necessarily dictate XML, but rather the set of messages that flow between services.

While XML, and SOAP by extension, are not prerequisites of SOA, the extensibility of XML makes the versioning of schema much easier.

# What Is a Service?

Besides being both the unit of design and the unit of deployment, services are surprisingly ill-defined for the size of the buzz surrounding SOA. Instead of defining what a service is, most of the literature describes properties of services. One such example is the four tenets of Service Orientation:

+   - Services are autonomous
+   - Services have explicit boundaries
+   - Services expose schema and contract, not class or type
+   - Service compatibility is determined based on policy

While these properties do indeed drive the design of scalable services (and will be discussed in more detail later), they apparently provide little guidance on the design of distributed systems. Architects just beginning to employ service-oriented techniques to their designs have no information about which elements should be grouped together into services, how to recognize and define service boundaries, and how these services are to be implemented using classic OO patterns. On top of that, the technologies surrounding the "pure" architectural aspects of SOA continue to be in a state of flux, and the various vendor offerings appear to be little more than repackaging of current products. Is it any wonder that SOA is already being dismissed as hype?

# What Goes in a Service?