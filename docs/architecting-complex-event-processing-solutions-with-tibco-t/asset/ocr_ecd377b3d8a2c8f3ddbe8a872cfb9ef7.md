# Obtain Claim Status

The behavior for Obtain Claim Status is shown in Figure 15-15.

# Summary

The Nouveau Health Care case study provides a coordinated set of example problems across the TIBCO Press architecture book series. The primary focus of the case study is the processing of health insurance claims. With the business model described in the case study, the processing of claims can be distributed across multiple parties. This creates the need for a Claim Tracker to centralize the status tracking for claims.

The Claim Tracker is involved in three processes: (1) monitoring the claim processing, (2) obtaining and returning claim status upon request, and (3) reporting exceptions to a process that resolves the exceptions.

The core of the Claim Tracker functionality is represented by a state machine associated with the Claim Status concept that is kept in the cache. This state machine shows the expected milestones of normal claim processing as well as exception states that are entered when service-level agreements are violated. Violations of these service-level agreements result in a Claim Processing Exception event being sent. The state machine also shows the recovery actions that are possible once an exception has occurred.

Since most of the monitoring logic is embedded in the state machine, the processing of a Claim Status Notification is straightforward. If it is a new claim, the Claim Status concept is created. Otherwise, the existing status is retrieved from the cache. In either case, the object is locked and a Status Report appended containing the details of the report. The RTC cycle is then allowed to process the event and drive the transitions in the state machine.

Timeouts in the state machine require their associated preprocessor functions to be specially registered. As with the normal processing, timeouts require the retrieval of the Claim Status from the cache and locking it prior to evaluating the state machine transitions in the RTC cycle.