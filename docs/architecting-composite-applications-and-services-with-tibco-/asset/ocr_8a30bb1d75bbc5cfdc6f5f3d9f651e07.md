# Architecture Patterns for Versioning

Services often act as intermediaries between components and back-end systems. Back-end systems often differ in their ability to provide and support multiple versions. This leads to a number of options for evolving the service when its back-end system is upgraded to a new version. The following sections discuss some of these options, all of which are variations on the architecture pattern shown in Figure 7-5.

# Accommodating a Compatible Change

If a change to a back-end system can be accommodated with a compatible change to the service interface, the original service can simply be replaced with the new version presenting the new version 1.1 interface (Figure 7-6). The new service interface supports the original clients as well as clients using the full capabilities of the new interface. Necessary changes are made within the service to utilize the new back-end interface, and the back-end system is replaced with the new version. Note that if there are multiple instances of the service, all must be upgraded to the new version before any of the clients are updated.

![](bbox=[0.3, 0.72, 0.7, 0.88])

Figure 7-5: Initial Architecture Pattern