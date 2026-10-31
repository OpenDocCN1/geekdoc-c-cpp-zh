
objects that are created and updated by inference agents. The resulting metrics reside in the cache.

Dashboard agents maintain the real-time data display in browsers. Data is displayed in charts and graphs. The configuration of each chart or graph includes the definition of a query that identifies the metrics that will be displayed. Optionally, charts and graphs may be configured to display visual alerts.

A special executable is used for processing units running dashboard agents. For best results, the inference, cache, and dashboard agents being used for maintaining a dashboard should be deployed in a cluster that is separate from the cluster used for the solution being monitored. Preferably this cluster should be deployed on different machines as well. This will prevent resource demand conflicts between the solution and the dashboard.

## Part III
## Design Patterns

This page intentionally left blank

## Chapter 10
### Solution Basics
### Objectives

This chapter focuses on basic capabilities you will require in crafting your solutions using TIBCO BusinessEvents®. After reading this chapter you will be able to

- Describe the various ways in which a change in a situation can be recognized and acted upon
- Describe how the sequencing or conditional execution of actions can be managed
- Describe how rules can be modified at runtime without halting your solution
- Explain the options available for exception reporting and logging
- Explain the naming guidelines for rules and rule functions

### Recognizing a Situation Change

Central to complex-event processing solutions is the recognition of a situation that requires action. Often this requires not just the recognition that a situation has arisen, but also a deeper understanding of how the situation has changed. Typically this recognition of change then becomes the trigger for further analysis.

This chapter presents several common design patterns for recognizing a situation change:

- Reference-Data Comparison pattern
- Reference-Data Change pattern
- State Machine Change Recognition pattern
- Continuous Query Change Recognition pattern

## Reference-Data Comparison Pattern

One approach to recognizing change is to compare current status against reference data (Figure 10-1). For example, a patient's current blood pressure is compared against an earlier reading to determine whether there has been a significant change.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_170_0.png)

Figure 10-1: Reference-Data Comparison Pattern

### Systems of Record for Reference Data

The reference data used in the Reference-Data Comparison pattern is generally historical data. The dominant design problem that arises in this pattern is that of maintaining the historical data. In crafting your solution, you need to answer three questions:

- 1. What is the system of record for the reference data?
- 2. How is the system of record being updated when the reference data changes?
- 3. How is the reference data made available to the CEP engine?

There are several possible approaches.

### TIBCO BusinessEvents® as Reference-Data System of Record

When you are using TIBCO BusinessEvents, answering the first question boils down to whether you want TIBCO BusinessEvents to be the system of record or some other system. If TIBCO BusinessEvents is to be the system of record, you’re going to end up with a pattern similar to that of Figure 10-2 for maintaining the reference data. Here the inference agent has a rule that updates the cache, which in turn updates the backing store. This is the pattern you get if you use the shared-nothing option or shared-all with write-behind option discussed in Chapter 6.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_171_0.png)

**Figure 10-2:** *TIBCO BusinessEvents® as Reference-Data System of Record*

## Database as Reference-Data System of Record

Another alternative is to use a database as the system of record (Figure 10-3). The TIBCO BusinessEvents® Data Modeling extension provides the facilities for automatically defining the cached concept representation of the reference data based on the database schema and the operations for updating the database and updating the cache from the database. This pattern makes the reference data available to other systems as well.

## External System as Reference-Data System of Record

A third alternative is to use an external system as the system of record for the reference data. A seemingly simple approach is shown in Figure 10-4, but there is a drawback: If some other entity changes the data in the external system, there is no mechanism for getting the change back into the cache.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_172_0.png)

Figure 10-3: Database as Reference-Data System of Record

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_172_1.png)

Figure 10-4: External System as Reference-Data System of Record—Naïve Approach

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_173_0.png)

Figure 10-5: External System as Reference-Data System of Record—Robust Approach

A more robust approach is shown in Figure 10-5. Here the inference agent updates the system of record, and an adapter (such as the TIBCO ActiveMatrix® Adapter for Database) recognizes the change and publishes a change notification. The inference agent picks up this change notification through a channel and updates the reference data accordingly.

## Reference-Data Change Coordination Patterns

The activities of comparing status to reference data and updating the reference data must be somehow coordinated. In a rule-based system, the simplest approach to performing these activities is to use separate rules for each activity (Figure 10-6a). This approach has a race condition and cannot guarantee that the comparison will finish (or even begin) before the reference data update occurs.

A more robust approach is to coordinate these two activities to ensure that the comparison completes before the update begins (Figure 10-6b). TIBCO BusinessEvents provides three mechanisms that can be used to ensure this sequencing.

- 1. Leave the two activities as separate rules and use rule priorities to ensure the proper sequence of execution (this is discussed later in this chapter).
- 2. Have a single rule that performs the two activities sequentially in the action part of the rule.
- 3. Use process orchestration as described in Chapter 8.

unless some preprocessor logic has explicitly brought the object into the agent's working memory. The typical sequence is that the arrival of an event triggers a rule that updates the object: The preprocessor for that event will bring the cached object into working memory.

In order for a rule to be subsequently triggered by a change to that object, this rule must be deployed in the same inference agent as the rule that made the change to the object. If rules are split up and deployed to different inference agents (as is frequently done in complex applications), you must bear in mind that rules triggered by the change in an object must be deployed to the same agent as the rules that modify the object when you decide which rules to deploy to which inference agents.

Note that this consideration applies to all types of objects: events, concepts (including those with associated state machines), scorecards, processes, and metrics. If you have an inference agent rule triggered by an object change, that rule must be deployed in the same inference agent that made the change to the object.

## State Machine Change Recognition Pattern

When the situation you are monitoring is modeled with a state machine, the machine itself can be used to announce changes in the situation (Figure 10-7). Transitions can be configured to send notifications. For example, the transition from Start to State X, which is taken when Event 1 occurs, can be configured to send Notification A when the transition is taken. States can also be configured to send notifications when they are entered or exited. For example, State X is configured to send Notification B when it is entered and Notification C when it is exited.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_175_0.png)

Figure 10-7: State Machine Change Recognition Pattern
