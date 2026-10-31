which are used to illustrate many of the points and design principles in this book.

# Nouveau Health Care Solution Architecture

Nouveau Health Care is a traditional health care insurance company. It sells health care insurance policies and covers claim payments with the revenue it collects from its premiums. It also administers the processing of claims.

There are factors that add to the complexity of Nouveau’s business. In some cases, the employers for whom Nouveau provides the health care benefits also provide the funds for paying the claims: Nouveau simply administers the policies. In other cases the administration of specialized services (vision and dental care) is farmed out to other companies. Both variations present some interesting design challenges.

# Nouveau Health Care Business Processes

Our use of Nouveau focuses on four of its business processes (Figure 4-1):

+   1. Validate Membership and its underlying Validate Membership Service
+   2. Manage Payments, which manages claim payments to health care service providers
+   3. Process Claim, and its initiator, Route Claim, which together handle the processing of insurance claims
+   4. Monitor Claim Processing, a process that monitors the execution of claim processing

The Validate Membership process is used by authorized parties (health care providers, employers, and members) to validate whether or not an individual was covered by the policy on a given date. This business process utilizes an underlying Validate Membership Service, which is also used by the Process Claim business process. Validate Membership is used as an example in the TIBCO® Architecture Fundamentals book.

The Manage Payments process manages the payments to health care service providers resulting from health care claims.¹ What makes