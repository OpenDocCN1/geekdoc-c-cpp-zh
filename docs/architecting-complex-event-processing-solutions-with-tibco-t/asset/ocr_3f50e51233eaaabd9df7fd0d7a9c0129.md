# Monitor Claim Processing

Figure 15-13 shows the processing of a Claim Status Notification event. This processing assumes that the Claim Status concept has a state machine configured as per Figure 15-8. The RTC cycle will evaluate the transitions of the state machine.

Figure 15-14 shows the behavior that occurs when an SLA timer expires. Since there is no channel and destination associated with the event, the preprocessor function must be specially registered using the Cluster.registerStateMachineTimeoutCallback() catalog function.

![](bbox=[0.35, 0.52, 0.65, 0.7])

Figure 15-12: Exception Reporting Interface

![](bbox=[0.1, 0.78, 0.95, 0.95])

Figure 15-13: Monitor Claim Processing Behavior