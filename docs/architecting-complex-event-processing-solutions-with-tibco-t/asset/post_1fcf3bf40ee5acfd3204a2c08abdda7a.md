
## Nouveau Health Care Solution Architecture

Nouveau Health Care is a traditional health care insurance company. It sells health care insurance policies and covers claim payments with the revenue it collects from its premiums. It also administers the processing of claims.

There are factors that add to the complexity of Nouveau’s business. In some cases, the employers for whom Nouveau provides the health care benefits also provide the funds for paying the claims: Nouveau simply administers the policies. In other cases, the administration of specialized services (vision and dental care) is farmed out to other companies. Both variations present some interesting design challenges.

## Nouveau Health Care Business Processes

Our use of Nouveau focuses on four of its business processes (Figure 15-1):

- 1. Validate Membership and its underlying Validate Membership Service
- 2. Manage Payments, which manages claim payments to health care service providers
- 3. Process Claim, and its initiator, Route Claim, which together handle the processing of insurance claims
- 4. Monitor Claim Processing, a process that monitors the execution of claim processing

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_238_0.png)

Figure 15-1: *Nouveau Health Care Business Processes*

The Validate Membership process is used by authorized parties (health care providers, employers, and members) to validate whether or not an individual was covered by the policy on a given date. This business process uses an underlying Validate Membership Service, which is also used by the Process Claim business process. Validate Membership is used as an example in the *TIBCO® Architecture Fundamentals* book.

The Manage Payments process manages the payments to health care service providers resulting from health care claims.[^1] What makes this process interesting is that, under normal circumstances, payments are made on a periodic basis (e.g., monthly) to health care service providers. This means that the payment manager must keep track of pending payments. By exception, payments to health care service providers for specific claims may be made immediately. The design of this process is explored in *Architecting Composite Applications and Services with TIBCO®*.

Process Claim and its related Route Claim process actually handle the processing of health care claims. Routing is required because some claims are processed by Nouveau itself while others are processed by partner companies. Process Claim is a consumer of both the Validate Membership Service and the services of the Payment Manager. Process Claim and Route Claim are used as examples in the upcoming book, *Architecting BPM Solutions with TIBCO®*.

Monitor Claim Processing keeps track of the progress of claim processing. This is necessary because some claim processing is done by partner companies. Monitoring provides uniform tracking of all health care claims regardless of whether Nouveau or one of its partners is handling the claim. This process is used as an example in this book.

## Nouveau Health Care Architecture Pattern

The business processes of Nouveau Health Care are executed by a collection of components (Figure 15-2). The Claim Router provides an interface for the Billing Provider to submit claims. It validates membership with the Membership Service, routes claims to the Claim Processor, and reports status to the Claim Tracker. The Claim Processor (and there may be more than one) adjudicates the claim, validating membership via the Membership Service, requesting claim payment via the Payment Manager, and reporting status to the Claim Tracker.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_240_0.png)

Figure 15-2: Nouveau Health Care Architecture Pattern for Claim Processing

The Payment Manager pays the service providers, getting the account associated with the plan from the Benefits Service, the account associated with the health care service provider from the Provider Service, and using the Banking Service to make the payments. It also reports status to the Claim Tracker.

## Nouveau Health Care in Context

Nouveau Health Care is part of a larger environment that includes the health care service providers that submit claims and the partner companies that process some of the claims (Figure 15-3). Here we see that there can be more than one claim processor, which explains the need for the Claim Router.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_241_0.png)

Figure 15-3: Nouveau Health Care Claim Processing in Context

## Processing Claims from Providers

Health care claims can be submitted by either the health care service provider or by the member to whom the service was provided. In the Nouveau Health Care example we focus on the claims submitted by providers and on the payments to those providers.

Figure 15-4 presents an overview of the processing of claims submitted by health care service providers. This sunny-day scenario shows provider interactions via the U.S. quasi-standard HIPAA transactions[^2] and shows deferred payments to the provider. The process model shows payer and provider account references, but not the details of the interactions with the Benefits Service and Provider Service required to obtain them. Similarly, it shows where membership is validated, but not the interactions with the Member Service that actually does the validation. Finally, for simplicity, all interactions with the Claim Tracker have been omitted.

Figure 15-4: Processing Claims from Providers

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_242_0.png)

Coordination Legend

- synchronous interaction
- asynchronous interaction
- delegation interaction

## Claim Tracker

The Claim Tracker is an example of a Track-and-Trace solution as described in Chapter 3. There are at least three processes associated with the Claim Tracker (Figure 15-5). The obvious process is Monitor Claim Processing—after all, that’s the whole point of the Claim Tracker. But monitoring doesn’t do any good if the resulting Claim Status is not made available to other participants. Thus a secondary process, Obtain Claim Status, is also required. However, even this is not enough. If the Claim Tracker determines that the process is not executing properly, it is best to proactively send a notification of the exception. This implies that there is yet a third process, Resolve Claim Processing Exception.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_243_0.png)

**Figure 15-5:** *Claim Tracking Processes*

While it may be obvious that the Claim Tracker is responsible for Monitor Claim Processing and Obtain Claim Status, it should be equally obvious that the tracker is not going to resolve the problems leading to the exception. Figure 15-6 shows the configuration of the Claim Tracker, clarifying the communications channels and indicating that the exception-resolver role is being played by a person and some as-yet unspecified interface.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_244_0.png)

Figure 15-6: Claim Tracker Configuration

Although we are not going to explore the exception-resolver role here, in practice it is very important to explore this role, for several reasons. Exploring the role will clarify the information that must be either present in the exception event or available via other interfaces in order to diagnose and fix the problem. Some of those interfaces may not exist! Furthermore, the interfaces required to take corrective action may not exist either! Exploring exception resolution will help you discover additional interfaces that will be required, and understand better the true scope of the project.

This design assumes that the claim processing participants are providing the requisite Claim Status Notifications. The next section will explore in more detail what notification is required and what information is retained in the Claim Status.

## Claim Status Concept

For any track and trace solution, a key task is to identify the important states of the item being tracked. The states are best thought of as milestones in the process being tracked. This will help you identify the appropriate level of detail. Figure 15-7 shows the state machine for claim tracking. The states represent the milestones. The transitions are labeled with the status being reported in the Claim Status Notification event.

Of course, this is just the sunny-day scenario. The most likely scenario for process breakdown is that the process simply gets stuck in a particular state. To detect this kind of breakdown, add SLA timers that start when each state is entered (Figure 15-8).

[^1]: In the real world, the Manage Payments process would also manage payments to members, reimbursing them for claim-related expenses that they have already paid themselves.

[^2]: In practice, each HIPAA transaction interface that is implemented by an enterprise is extended to accommodate the specific requirements of that enterprise.
