# Distributed Federation Pattern

A more general pattern for geographically distributed federation is shown in Figure 17-3. Here each site has its own federated service domain that provides local access to all federated services. When the actual service resides at another site, it is re-exposed through the local federated service domain. This approach consolidates all inter-site routine into the federated domains.

In distributed federation, each site maintains its own local repository of federated services, or at least its own local interface to that repository. Most of the repository content will be the same at each site, either replicated or using links to reference the source materials at a single site. Unique to each repository are the endpoints for accessing the federated services.

![](bbox=[0.123, 0.457, 0.938, 0.847])

**Figure 17-3:** *Distributed Federation Pattern*