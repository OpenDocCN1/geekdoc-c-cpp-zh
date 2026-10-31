![](bbox=[0.2, 0.14, 0.8, 0.5])

Figure 4-16: Claim Payment Request and Response

The Claim Payment Response is used in both interfaces. For immediate payments, the paidAmount in the Service Instance Payment Result will contain the amount actually paid. For deferred payments, this field will be zero and the pendingAmount will indicate the amount that will be paid upon settlement. When this data structure is returned by the Claim Payment Notification Interface, the pendingAmount will be zero and the paidAmount will indicate the amount that was actually paid.

# Payment Manager Specification: Processes

# Immediate Payment Process

An overview of the process that the Payment Manager uses for immediate payment is shown in Figure 4-17. Upon receipt of the request, the Payment Manager obtains a settlement account. For each service instance the payer account is found, the provider settlement record is obtained, and the funds are transferred from the payer account to the settlement account. Note that, by business rule, failed transfers do not keep other transfers from proceeding. With respect to the Provider Settlement Record, if one has not been created in this instance of the immediate payment process, one is created. Otherwise, the existing