cash dispensers. A strategy is needed that causes as little disruption to the established three-tier architectures of the two organizations as possible.

You are asked first to provide a simple ODP specification of the two systems, and then to identify the minimum set of changes that will be required to implement the modifications in both systems.

# ### B.1.6 Google Search Engine

Imagine that you are hired by Google™ as Chief Architect for one of its core products, the Google Search Engine, and that they want you to provide an architectural description of that application, with the goals of:

+   - Relying on high-level models to understand this application, in a platform- and technology-independent manner.
+   - Having a conceptual model of the data the application manages.
+   - Defining the software architecture of the application, for guiding subsequent developments and changes.
+   - Specifying the deployment architecture and communications infrastructure, expressed in terms of distributed servers, processes and channels, to be able to have a global picture of the system workload, to perform load-balancing improvements or to conduct end-to-end performance analysis of the system.
+   - Describing the technology adoption, acquisition, provisioning and maintenance procedures for the hardware, software and communications infrastructure that should support the application.

Write the ODP specification of the Google Search Engine, including all five viewpoints and the correspondences between them.

# ### B.2 Some Additional Questions

Answer these questions based on the concepts presented in this book.

+   1. A designer says, “Now that we have decided to allow persistent data to be stored on mobile devices in our system, the enterprise policy on required availability levels means we will need to add engineering mechanisms supporting replication transparency for all the computational objects, not just those that are currently tagged as having critical requirements in the computational design.” Explain, to someone ignorant of the ODP architecture, what the designer is saying, and what the concepts they have used mean.