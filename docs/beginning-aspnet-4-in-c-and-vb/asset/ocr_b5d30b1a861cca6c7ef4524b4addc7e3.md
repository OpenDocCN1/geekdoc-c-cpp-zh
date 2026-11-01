![](bbox=[0.07, 0.13, 0.7, 0.57])

FIGURE 52-2

# Domain Controller

A single domain can have multiple domain controllers, each of which stores all of the objects in the domain. There is no master server, and all DCs are treated equally; you have a multimaster model. The objects are replicated across the servers inside the domain.

# Site

A site is a location in the network that holds at least one DC. If you have multiple locations in the enterprise, which are connected with slow network links, you can use multiple sites for a single domain. For backup or scalability reasons, each site can have one or more DCs running. Replication between servers in a site can happen at shorter intervals because of the faster network connection. Replication is configured to occur at larger time intervals between servers across sites, depending on the speed of the network. Of course, replication intervals can be configured by the domain administrator.

# Domain Tree

Multiple domains can be connected by trust relationships. These domains share a common schema, a common configuration, and a global catalog (more on global catalogs shortly). A common schema and a common configuration imply that this data is replicated across domains. Domain trees share the same class and attribute schema. The objects themselves are not replicated across domains.

Domains connected in such a way form a domain tree. Domains in a domain tree have a contiguous, hierarchical namespace. This means that the domain name of the child domain is the name of that child domain appended to the name of the parent domain. Between domains, trusts using the Kerberos protocol are established.

For example, you have the root domain wrox.com, which is the parent domain of the child domains india.wrox.com and uk.wrox.com. A trust is set up between the parent and the child domains, so that accounts from one domain can be authenticated by another domain.