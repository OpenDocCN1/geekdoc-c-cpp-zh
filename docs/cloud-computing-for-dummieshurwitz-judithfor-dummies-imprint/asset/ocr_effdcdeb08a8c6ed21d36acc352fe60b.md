# Hybrid environments

Your company will probably have a *hybrid* environment: a traditional data center, a private cloud, and some cloud services. That hybrid is part of what makes cloud management so complex. They may use virtualized servers as well as dedicated physical servers.

Chapter 17 defines *virtualization* as using computer resources to imitate other computer resources or even whole computers. The term is very broad and can include virtualizing everything from memory to software, but we keep it simple for right now.

This hybrid environment requires management of both the virtual servers and the physical infrastructure beneath. And, because there is a good chance that most enterprises won’t move *all* of their computing resources to the cloud, they have to be concerned with how this hybrid environment gets managed. Two important capabilities need to be in place to manage this hybrid world: the service catalog and the Configuration Management Database (CMBD).

# The service catalog

One of the important factors in managing a cloud is to ensure a way to manage IT assets and activities. Enter the service catalog (defined as part of the *Information Technology Infrastructure Library [ITIL] Service Design* best practice). The catalog is a component list that makes up internal and external services that are available to an organization.

A typical service catalog includes such items as the definition of the service, its service level, who is entitled to use that service, and what components are required to execute that service. Clearly, a service catalog is required for organizations to manage services in a hybrid world — across data centers, private and public clouds, as well as hosted environments. The service catalog is an essential tool for both cloud providers and customers that need a view into the assets they are using. Many cloud providers package a service catalog to help their customers work between their cloud and external resources.

# The Configuration Management Database (CMDB)

To understand what services are being managed across your various computing environments, you should keep track of changes. That is the role of the *Configuration Management Database (CMDB)*. For example, many cloud environments use extensive virtualization to add efficiency. Virtualization enables the abstraction of hardware assets so that these assets can be used for multiple purposes. These varied uses increase the difficulty of tracking changes to these resources. However, it’s important for the cloud provider (even if that’s you in your private cloud) to track these assets and understand what’s been changed and what state that service is in.