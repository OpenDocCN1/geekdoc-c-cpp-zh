To further illustrate the operational level, as shown in Figure 13.12, let's have a closer look at a process step example for creating an order.

# Operational Level – Process Steps

At the operational level we have the process steps with variants as described next:

+   - **Variant 1**
+     If, for example, a call center sales employee gets a call (input), he will ask the customer for his name and required products (collect), check prices and give a discount (approve), complete the sales order (store), and confirm the order to the customer (inform).
+   - **Variant 2**
+     The SAP system receives an electronic data interchange (EDI) order from a customer (input). The system searches for additional information to create the order in the system (collect). Based on pricing rules, the order is approved automatically or a flag is set for manual approval (approve), the sales order is released (store), and an EDI confirmation is sent to the customer (inform).
+   - **Variant 3**
+     A customer sends an email with his order (input). A call center employee checks and fulfills the order with the proposed discount (collect). An offline form is sent to the manager for manual approval (approve), the sales order is created and released on the approved form (store), and an email confirmation is sent to the customer (inform).

The results of all three process step variants are similar, but the implementation of activities and the required resources (technology and people) are different. The examples show you the difficulty of describing the processes. Variant 1 describes the way a person works behinds his desk. Variant 2 describes how the system handles the request automatically, and Variant 3 shows how people work together to get the order in the system. Level 5 is the only place where business process requirements and implementation can be decoupled. It is the preferred place to measure process performance and to compare process steps in a generic way.

# Operational Level – Process Activities

From a business perspective, process flows are described with events and functions, for example, with an event-driven process chain (EPC) in ARIS. The process