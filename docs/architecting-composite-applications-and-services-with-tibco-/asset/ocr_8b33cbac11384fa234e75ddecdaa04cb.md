a service provider residing on the same node and other service providers residing on other nodes.

ActiveMatrix BusinessWorks and its companion ActiveMatrix BusinessWorks Service Engine have four thread pools of interest:

+   1. Engine thread pool
+   2. Zero or one Tomcat thread pool
+   3. Zero or one HTTP Component thread pool
+   4. Invoke Partner thread pool

The engine thread pool is the one that executes jobs in an ActiveMatrix BusinessWorks engine. The Tomcat or HTTPComponent thread pools are used for HTTP connections directly to the BusinessWorks engine (i.e., not through the ActiveMatrix Service Bus). The Invoke Partner thread pool is used for outbound calls from BusinessWorks to the ActiveMatrix Service Bus.

There are a number of engine-level parameters that can be used to tune ActiveMatrix BusinessWorks. These include

+   - Max Jobs
+   - Activation Limit
+   - Flow Limit
+   - Step Count

For JMS process starters, there are additional tuning parameters:

+   - Acknowledge Mode
+   - Max Sessions