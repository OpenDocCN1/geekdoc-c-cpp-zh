![](bbox=[0.12, 0.14, 0.9, 0.48])

Figure 10-5: External System as Reference-Data System of Record—Robust Approach

A more robust approach is shown in Figure 10-5. Here the inference agent updates the system of record, and an adapter (such as the TIBCO ActiveMatrix® Adapter for Database) recognizes the change and publishes a change notification. The inference agent picks up this change notification through a channel and updates the reference data accordingly.

# Reference-Data Change Coordination Patterns

The activities of comparing status to reference data and updating the reference data must be somehow coordinated. In a rule-based system, the simplest approach to performing these activities is to use separate rules for each activity (Figure 10-6a). This approach has a race condition and cannot guarantee that the comparison will finish (or even begin) before the reference data update occurs.

A more robust approach is to coordinate these two activities to ensure that the comparison completes before the update begins (Figure 10-6b). TIBCO BusinessEvents provides three mechanisms that can be used to ensure this sequencing.

+   1. Leave the two activities as separate rules and use rule priorities to ensure the proper sequence of execution (this is discussed later in this chapter).
+   2. Have a single rule that performs the two activities sequentially in the action part of the rule.
+   3. Use process orchestration as described in Chapter 8.