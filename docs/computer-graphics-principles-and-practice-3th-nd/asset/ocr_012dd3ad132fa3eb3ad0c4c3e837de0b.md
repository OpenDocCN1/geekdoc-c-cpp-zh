![](bbox=[0.067, 0.109, 0.677, 0.304])

*Figure 16.10: Sample distribution of AMIP responsibilities in an application using retained-mode middleware.*

![](bbox=[0.125, 0.409, 0.666, 0.721])

*Figure 16.11: Abstract depiction of an RM layer providing two types of optimization discussed in Section 16.4.2 (view-frustum culling and IM-instruction reuse), showing the synchronization logic that ensures the acceleration data structures (BVH and IM-instruction cache, in this example) are updated when the scene graph is modified.*

because the structures must be maintained as the scene graph is modified, requiring sophisticated logic to avoid unnecessary invalidations (i.e., premature discarding) of cached information, and to avoid the expense of wholesale regeneration of the structures.

In addition to the CPU time allocated to maintaining these structures, there is also a nontrivial CPU memory cost as well. At the end of this section, we’ll revisit the issue of the runtime cost of scene-graph middleware and discuss the cost/benefit tradeoffs.