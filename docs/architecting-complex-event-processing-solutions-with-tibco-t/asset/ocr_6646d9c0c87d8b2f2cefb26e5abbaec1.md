![](bbox=[0.15, 0.13, 0.92, 0.68])

Figure 5-23: Postprocessing Behavior—Multi-Threaded

Figure 5-23 shows the behavior with multi-threading. All the activities run in parallel, with the event output and cache update activities using threads from the Agent.threadcount thread pool and the database update (if required) using threads from the Agent.dbthreadcount pool.

# ACEPSTLocalChannel Example

The ACEPSTLocalChannel example illustrates several features, including

+   - Configuring a processing unit with two inference agents
+   - The use of local channels
+   - Rule actions publishing events
+   - Preprocessor functions creating and consuming events