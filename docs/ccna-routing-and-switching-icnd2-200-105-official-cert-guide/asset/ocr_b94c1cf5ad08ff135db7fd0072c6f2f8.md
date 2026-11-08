Summarizing the key features of shapers:

+   - Shapers measure the traffic rate over time for comparison to the configured shaping rate.
+   - Shapers allow for bursting after a period of inactivity.
+   - Shapers are enabled on an interface for egress (outgoing packets).
+   - Shapers slow down packets by queuing them, and over time releasing them from the queue at the shaping rate.
+   - Shapers use queuing tools to create and schedule the shaping queues, which is very important for the same reasons discussed for output queuing.