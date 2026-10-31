# Nouveau Health Care Solution Architecture

Nouveau Health Care is a traditional health care insurance company. It sells health care insurance policies and covers claim payments with the revenue it collects from its premiums. It also administers the processing of claims.

There are factors that add to the complexity of Nouveau’s business. In some cases, the employers for whom Nouveau provides the health care benefits also provide the funds for paying the claims: Nouveau simply administers the policies. In other cases, the administration of specialized services (vision and dental care) is farmed out to other companies. Both variations present some interesting design challenges.

# Nouveau Health Care Business Processes

Our use of Nouveau focuses on four of its business processes (Figure 15-1):

+   1. Validate Membership and its underlying Validate Membership Service
+   2. Manage Payments, which manages claim payments to health care service providers
+   3. Process Claim, and its initiator, Route Claim, which together handle the processing of insurance claims
+   4. Monitor Claim Processing, a process that monitors the execution of claim processing

![](bbox=[0.109, 0.658, 0.891, 0.911])

Figure 15-1: *Nouveau Health Care Business Processes*