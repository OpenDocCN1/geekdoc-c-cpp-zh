# Reference Architecture Example – UI Simplification on Single Legacy Backend

In our example we assume the typical project situation: We have a backend system with business functionality and local/remote programming interface technology, but it is not service-enabled in the sense of SOA. Let's assume we need a simplified user interface for a given business process, which is supported by this backend system. Based on the pattern catalog, we can sketch many architectural drafts to fulfill these requirements. The most typical solutions for this category of use cases look like the following.

Either use the backend UI technology to provide an additional user interface, which is a subset of the fields or functionality of the given user interface (see Figure 16.12) or enrich the landscape with a dedicated consumption frontend with dedicated state-of-the-art user interface technology and connect this frontend to the backend system, which must be service-enabled first (see Figure 16.13). Alternatively, we can replace the service enabling by an additional enterprise service bus, which offers an adapter to translate the legacy programming interface of the backend system (see Figure 16.14).

![](bbox=[0.17, 0.53, 0.42, 0.88])

Figure 16.12 UI Simplification Reference Architecture – Simple System