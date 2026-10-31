There are several ways in which the profiler can be turned on and off. These include the following:

+   - TIBCO BusinessEvents Monitoring and Management: This application provides an interactive mechanism for turning profiling on and off.
+   - Agent properties: The `be.engine.profile...` family of properties can be used to statically configure profiling. These properties are applied when the agent starts.
+   - TIBCO Hawk®: Each agent has an embedded Hawk microagent interface that includes operations for turning profiling on and off. The Hawk console can be used to interactively control profiling, or Hawk rules can be written to turn profiling on and off when specific conditions exist.
+   - Catalog functions: Catalog functions are provided that turn profiling on and off. These can be incorporated into preprocessor functions or rule actions.

Profiling is an essential tool for understanding the performance implications of your design. However, just turning the profiler on will not necessarily provide you with the information you require. Many performance issues will not be apparent unless there are a significant number of objects in the memory and/or cache. You need to analyze your solution and determine the worst-case peak-condition number of objects, and then observe the behavior under those conditions. This may require a special test to simulate those conditions.

# Design Choices and Agent Performance

There are a number of design choices that can impact performance, including

+   - Structuring rule conditions
+   - Organizing decision tables
+   - Accessing large XML event payloads
+   - Locking objects
+   - Choosing threading models
+   - Using synchronous I/O calls in rule actions