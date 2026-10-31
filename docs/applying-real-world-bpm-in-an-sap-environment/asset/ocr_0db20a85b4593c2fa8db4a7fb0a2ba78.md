| Merged Web Dynpro DC | Separate DCs |
|---|---|
| \\all (a WD DC consisting of four WD connections) | 31.609 seconds |
| \\change | 7 seconds |
| \\create | 6.328 seconds |
| \\result | 11.141 seconds |
| \\search | 25.578 seconds |
| Sum | 50.47 seconds |

Table 14.2  Comparison of Build Times

What becomes very obvious is the fact that the build of a DC has some overhead. Opting for too many DCs will therefore create problems during build time.

The structure of the DCs of a composite application is therefore always a compromise between the guidelines for business separation of logic in DCs (as small as possible according to the business needs) and the overhead of the infrastructure for each DC. There is normally a conflict between optimizing either the number of DCs for the fastest overall build (as few DCs as possible) or the fastest build for developers (as many DCs as possible). The numbers in the table should provide some guidance about how much the additional overhead for development would be. If the decision is to use the more coarse-grained DC design, the build times for developers will increase. If the decision is to use fine-grained DCs, the overhead of the infrastructure (build time and maintenance of DC dependencies between the DCs) will increase. It is therefore important to make a balanced decision.

The actual guidelines are highly dependent on the application use case, but you still have to take into account the build time and infrastructure aspects during the decision process of the composite application structure.

# Clustering of Content

Usually a composite application contains a lot of entities of one programming model, such as Web Dynpro components and EJBs. The recommendation is to put entities that are highly related into one DC. This does not mean all components are put into one DC. In principle, it is a question of how to cluster the components in DCs. A cluster belongs in one DC. If the connection between two potential clusters is very weak (only one or two dependencies), the components are put into two DCs. This recommendation can be defined as follows: