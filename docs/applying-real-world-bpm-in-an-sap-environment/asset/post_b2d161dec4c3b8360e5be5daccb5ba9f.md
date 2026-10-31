
Responsibility roles involved creates the RACI model. This matrix provides information on the simple and complex roles with regard to activities performed in the process step. If a RACI role contains different activities, it must be established if these activities can be combined. Table 13.5 shows activities that can be combined in a single responsibility role.

Table 13.5 Valid Combined Activities

| Combined Activities |
|---|
| Collect + Approve |
| Collect + Approve + Store |
| Collect + Approve + Store + Inform (transaction pattern) |
| Approve + Store |
| Approve + Store + Inform |
| Store + Inform |

Other combinations usually require different actors to be involved in the process step and often lead to the development of additional or changed activity flows. This might be the case when subsequent approval steps are involved or when collection of data is executed by different actors. Applying the RACI model together with the ICASIO pattern thus identifies omissions in the description of the activity flow of the process step and leads to the definition of process step variants. The reasons for the development of these process step variants can be found in localization, regulation, and/or application support. Just keep in mind that a process step variant can have only one “store” activity (single or combined) to be defined correctly.

A good example is the sales order process that can be handled fully automated by the customer (Web shop) or through the company’s back office. For the online variant, the customer is responsible for the process (create the order, store the order), and he collects relevant information (product information, address, and payment data). In the backend a real-time inventory check is performed, a sales order is created, and a sales order confirmation is sent out as a generated PDF via email. The implicit approval of the order comes from business rules, and the handling of the payment is the responsibility of the online payment provider. On the other end of the spectrum, the customer might decide to use a more traditional approach and contact his account manager. The account manager now becomes responsible for the sales order process. He collects the required information and checks with the warehouse for the inventory and the customer support desk for the credit check. The company’s back office is responsible for entering the data in the sales application, and a line manager has to approve the order before it is executed. Between these two extremes, many variants might exist, with different people involved, and shifting responsibilities emerge from applying the RACI model in combination with the ICASIO pattern.

Using the ICASIO pattern and creating the RACI model for the process step helps identify the differences in activity flows and provides insight to opportunities for harmonization of processes and process steps.

Now that we understand the relationship between RACI and the ICASIO pattern, let's summarize. The ICASIO pattern helps you to identify a process step with its activities in a generic way within a business process. The process step has different variants depending on the flow of its activities. RACI helps you identify the completeness of the process step and its variants. Each role must be part of one or more process step variants, and all activities must have at least one role. RACI and ICASIO together simplify and validate your process work and can be used in workshops to collect the relevant information about processes.

## 13.2.10 Process Identification and Harmonization on the Operational Level

Now that we know the importance of harmonization of process steps (variants) and have identified the advantages of using the ICASIO pattern and the RACI model for the detailed description of the process step (variants), let's have a closer look at process harmonization on the operational level.

![](img/30a88f75957f887ca511028d178ca5c7_331_0.png)

Figure 13.12 Defense Example of Level 5 Processes

To further illustrate the operational level, as shown in Figure 13.12, let's have a closer look at a process step example for creating an order.

## Operational Level – Process Steps

At the operational level we have the process steps with variants as described next:

- **Variant 1**
  If, for example, a call center sales employee gets a call (input), he will ask the customer for his name and required products (collect), check prices and give a discount (approve), complete the sales order (store), and confirm the order to the customer (inform).
- **Variant 2**
  The SAP system receives an electronic data interchange (EDI) order from a customer (input). The system searches for additional information to create the order in the system (collect). Based on pricing rules, the order is approved automatically or a flag is set for manual approval (approve), the sales order is released (store), and an EDI confirmation is sent to the customer (inform).
- **Variant 3**
  A customer sends an email with his order (input). A call center employee checks and fulfills the order with the proposed discount (collect). An offline form is sent to the manager for manual approval (approve), the sales order is created and released on the approved form (store), and an email confirmation is sent to the customer (inform).

The results of all three process step variants are similar, but the implementation of activities and the required resources (technology and people) are different. The examples show you the difficulty of describing the processes. Variant 1 describes the way a person works behind his desk. Variant 2 describes how the system handles the request automatically, and Variant 3 shows how people work together to get the order in the system. Level 5 is the only place where business process requirements and implementation can be decoupled. It is the preferred place to measure process performance and to compare process steps in a generic way.

## Operational Level – Process Activities

From a business perspective, process flows are described with events and functions, for example, with an event-driven process chain (EPC) in ARIS. The process step variant has a flow of one or more process activities (level 6). See Figure 13.13 for an example of level 6 processes.

![](img/30a88f75957f887ca511028d178ca5c7_333_0.png)

**Figure 13.13** Defense Example of Level 6 Processes

The process step variant is described with the following activity types:

- **Collect**
  Gather data required for fulfilling the activity or task.
- **Approve**
  Confirm the correctness and completeness of the gathered data.
- **Store**
  Persist the gathered data in an application.
- **Inform**
  Provide feedback on the activity to the actors involved in the process step or a combination of those types in one activity.
- **Meeting**
  Collect and approve with more approvers (people) parallel.
- **Transaction**
  Collect, approve, store, and inform in a single activity.

Patterns can be found that can be reused in other variants and that make measurement and comparison of process characteristics across the different process activities possible. Figure 13.14 shows an example of the process group to business process step variant and activities.

![](img/30a88f75957f887ca511028d178ca5c7_334_0.png)

Figure 13.14 Example from Process Group to Business Process Step

## Variant and Activities

IT must implement the process activities of the process step flow shown in Figure 13.14. A canonical data model is needed as an overlay over the existing IT landscape. It should describe the business objects and their attributes and methods in a generic way, independent from the underlying IT solution. These generic business objects describe the process data (input/output) of the activity and are used to define the independent definition of business objects for a business domain. This creates the basis for loosely coupled domain services. Business Process Modeling Notation (BPMN) can be used to describe these detailed flows (see Figure 13.15), because it assigns the resources to the activities, handles errors and exceptions, and is eligible for execution.

## Operational Level – Process Tasks

The three process step variant examples show us that for executable processes, description of an activity alone is not enough. For translation to the IT requirements, we need to know if the activity is a human task, an automatic task, a decision-making task, or a combination of tasks. The activity within a process step
