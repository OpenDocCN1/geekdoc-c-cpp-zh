![](bbox=[0.07, 0.12, 0.95, 0.53])

Figure 15-6: Claim Tracker Configuration

Although we are not going to explore the exception-resolver role here, in practice it is very important to explore this role, for several reasons. Exploring the role will clarify the information that must be either present in the exception event or available via other interfaces in order to diagnose and fix the problem. Some of those interfaces may not exist! Furthermore, the interfaces required to take corrective action may not exist either! Exploring exception resolution will help you discover additional interfaces that will be required, and understand better the true scope of the project.

# Claim Status Concept

For any track and trace solution, a key task is to identify the important states of the item being tracked. The states are best thought of as milestones in the process being tracked. This will help you identify the appropriate level of detail. Figure 15-7 shows the state machine for claim tracking. The states represent the milestones. The transitions are labeled with the status being reported in the Claim Status Notification event.

Of course, this is just the sunny-day scenario. The most likely scenario for process breakdown is that the process simply gets stuck in a particular state. To detect this kind of breakdown, add SLA timers that start when each state is entered (Figure 15-8).