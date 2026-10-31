dedicated to the component. The fact that the database is not part of the composite actually reflects a change to the specification for the Payment Manager, as it introduces an external component upon which the Payment Manager depends. The logical and physical design of the ODS is part of the Payment Manager, but its implementation depends upon a database that is operated independent of the Payment Manager.

The Payment Manager Composite comprises four components: the Claim Payment Service Implementation, the Settle Deferred Payments Implementation, the Settlement Service Implementation, and the Notification Router.

The Claim Payment Service Implementation is the component that handles invocations of the Claim Payment Interface. For immediate payments it manages the entire process, utilizing the Settlement Service to make the actual payments. For deferred payments, it leaves the state of the pending settlements in the ODS.

The Settle Deferred Payments Service Implementation periodically settles payments that have been deferred. Note that it does not have a service interface: Its behavior is driven by timers, not invocations by other components. It also uses the Settlement Service to actually make the payments.

The Settlement Service Implementation embodies the mechanics of making payments to health care service providers. It is a shared service that is used by both the Claim Payment Service Implementation and the Settle Deferred Payments Service Implementation, since both of these components require this capability.

The Notification Router takes asynchronous notifications of claim payments and routes them to the appropriate party. Note that as additional parties are added at the business level, additional routing entries will need to be made.

# Composite Behavior Management: Orchestration and Choreography

The overall behavior to be exhibited by the Payment Manager is described by the triggered behavior descriptions contained in its specification (Chapter 6). What must be described by the Payment Manager architecture is how the components of the Payment Manager collectively produce that behavior. A key decision to be made is what approach to take in coordinating the work of these components.