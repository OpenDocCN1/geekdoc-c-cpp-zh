![](bbox=[0.08, 0.18, 0.92, 0.68])

# Figure 3-14: Response Orchestration Pattern

pattern, process orchestration is used to coordinate multiple participants in responding to a situation. The reason for the orchestration is twofold: to control the order in which the actions are performed and to confirm the successful completion of the actions. Less common is a situation in which process coordination is required for situation recognition.

This pattern is a hybrid of event-driven and request-driven interactions. All of the interactions up to the receipt of the situation recognition announcement are event driven. The response orchestration component, however, uses request-driven interactions to not only request that each participant perform its work but also to confirm the successful completion of that work.

When this pattern is used, a choice must be made regarding the type of technology to be used for the response orchestration. Traditionally, this would be a component designed specifically for process orchestration, such as TIBCO ActiveMatrix BusinessWorks™ or TIBCO ActiveMatrix® BPM. With this approach, if rule-based reasoning is required in the orchestration, the Decision-as-a-Service pattern is used. The service returns values that then guide the subsequent process execution.