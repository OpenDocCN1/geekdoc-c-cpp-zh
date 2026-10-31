# Nouveau Health Care Architecture Pattern

The business processes of Nouveau Health Care are executed by a collection of components (Figure 4-2). The Claim Router provides an interface for the Billing Provider to submit claims. It validates membership with the Membership Service, routes claims to the Claim Processor, and reports status to the Claim Tracker. The Claim Processor (and there may be more than one) adjudicates the claim, validating membership via the Membership Service, requesting claim payment via the Payment Manager, and reporting status to the Claim Tracker. The Payment Manager pays the service providers, getting the account associated with the plan from the Benefits Service, the account associated with the health care service provider from the Provider Service, and using the Banking Service to make the payments. It also reports status to the Claim Tracker.

![](bbox=[0.2, 0.5, 0.9, 0.9])

Figure 4-2: Nouveau Health Care Architecture Pattern