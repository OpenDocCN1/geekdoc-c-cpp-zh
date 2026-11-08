First, the HSRP rules. When a router (call it the local router) has an HSRP-enabled interface, and that interface comes up, the router sends HSRP messages to negotiate whether it should be active or standby. When it sends those messages, if it...

+   - **Step 1.** ...discovers no other HSRP routers in the subnet, the local router becomes the active router.
+   - **Step 2.** ...discovers an existing HSRP router, and both are currently negotiating to decide which should become the HSRP active router, the routers negotiate, with the router with the highest HSRP priority becoming the HSRP active router.
+   - **Step 3.** ...discovers an existing HSRP router in the subnet, and that router is already acting as the active router:
+     - **A.** If configured with no preemption (the default: **no standby preempt**), the local router becomes a standby router, even if it has a better (higher) priority.
+     - **B.** If configured with preemption (**standby preempt**), the local router checks its priority versus the active router; if the local router priority is better (higher), the local router takes over (preempts) the existing active router to become the new active HSRP router.