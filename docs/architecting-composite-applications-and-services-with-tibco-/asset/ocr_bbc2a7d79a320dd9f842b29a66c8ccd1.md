# Composite Architecture Pattern

The architecture pattern for the composite defines the components of the composite and the manner in which the interfaces of those components are wired together. The composite wiring defines the architecture pattern of the composite. It identifies the components, their interfaces, and the communications channels between the interfaces.

Figure 13-1 shows the architecture pattern for the Payment Manager. This pattern has two primary components: a Payment Manager Composite and an Operational Data Store (ODS). In this design, the ODS is not shown as part of the Payment Manager Composite. This is typical when the physical instance of the database to be used is not

![](bbox=[0.1, 0.58, 0.9, 0.92])

Figure 13-1: Payment Manager Architecture Pattern