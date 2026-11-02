
Secondly, the enterprise language accommodates the expression of business services. A **business service** is a particular description of behaviour that focuses on the functionality or capability provided by one party to the others who can then use the service to satisfy their own business needs, resulting in some added value to them. A business service can be provided by a single role in a community or it may involve several roles; for example, the phone repair service of the **Phone Repair** community is provided by the **Phone Repair Provider** role (encompassing **HQ system** and **Branch staff** roles of the **Detailed Phone Repair** community jointly), which both interact with the service users. This business service is the central part of the **Phone Repair** community and can be used by other members in the **Phone Repair** community, such as the **Customer** and the **User**.

Business services can be made public by a community; that is to say, they can be used not only by the objects filling other roles in the same community but may also be accessed by the behaviour of different communities. Note that a business service can be supported by one or more technical services, described in the computational viewpoint, and that these different uses of the concept of service are in line with the current SOA frameworks, such as the **OASIS Reference Architecture** [46].

A **process** is a specific form of behaviour expressed in terms of sequential or concurrent ordering between **steps**. Each business step may consume and produce information. A process will thus involve one or more community roles, which perform actions associated with business steps. Each process is aimed at satisfying an objective, and many processes can be defined in a community, each of which contributes to the overall objective of the community. This abstract definition of the process can be further refined to give more detailed process definitions represented in notations such as BPMN, or UML activity diagrams (as in UML4ODP).

**Interactions** are the basic elements of the community behaviour. Each interaction indicates which roles it involves, and what part they each play in it. For example, in a message exchange requesting a repair, the community roles of **User** and **Branch staff** may be involved, with the user acting as initiator and the branch as responder (where initiator and responder are interaction roles, not community roles). Multiple interactions can then be composed into sequences or concurrent activities, forming extended pieces of behaviour, building up first steps and then complete processes. Thus, simple interactions can be used to build up control flows, yielding a style of behaviour familiar from process modelling.

The complete behaviour of a community can generally be decomposed into a number of distinct processes. In the PhoneMob (see figure 2.7), we have, for example, the repair process, concerned with dealing with a faulty phone, and two separate administrative processes, one dealing with the negotiation of service levels with a logistics provider and the other providing assessment and reporting of key performance indicators. Finally, we have a management process concerned with the maintenance of the phone loan policy.

![](img/b3a2d21424654c9a1d0654b2dce50e07_72_0.png)

### 2.6.1 A Community Process

Let us look further at one of the constituent processes in the community behaviour. Figure 2.8 shows the definition of the process concerned with the lifecycle of a single phone repair, in the case of a VIP user who is entitled to

![](img/b3a2d21424654c9a1d0654b2dce50e07_72_1.png)
![](img/b3a2d21424654c9a1d0654b2dce50e07_73_0.png)

be issued a loan phone while her own is being dealt with. The roles involved are the user, phone repair provider, logistics provider and phone supplier. The Phone Repair community has other roles, but they are not directly involved in this process.

Several of the flows in this figure are marked as referencing a user handset as an artefact, shown as an «EV Artefact»; the flow from the Request Repair step is one example. In this specification, we have chosen to use an artefact reference to highlight the fact that the flow is associated with the physical transfer of the handset concerned between roles. After the request repair step not only does the process flow transfer to the phone repair provider, but also responsibility for the broken handset is transferred. Note that the artefact is decorated with its assumed state [broken]; this state is drawn from the state machine defined for handsets (see figure 2.9). In places where the state is uncertain, such as on the return of the loan handset, this decoration is omitted.

The steps in this representation of the process are comparatively coarse grained. Thus, for example, the detail involved in saving the user's state and SIM is subsumed into the Handle Request step when the phone is first received, and the restoring of this state forms part of the Prepare Return step. These details are important in ensuring the user receives a high quality experience, but the choice of exactly what order the necessary actions are taken in is not of concern to the user or customer roles.

### 2.6.2 Refining the Process

The behaviour shown in figure 2.8 is generic; it applies to all repair activities in the organization and is expressed in terms of the roles shown in figure 2.2. It can be refined by each branch independently, in ways that suit their local situation. Figure 2.10 shows one such refinement, defining the

![](img/b3a2d21424654c9a1d0654b2dce50e07_74_0.png)

FIGURE 2.10: The repair process as seen from one of the branches.

Branch Repair Provision community. This community has a community object that offers one way of fulfilling the top-level branch role.

This process adds detail; it now distinguishes between the different internal roles of the PhoneMob organization, using the refined roles shown in figure 2.4. However, the process as seen by the external parties should be essentially

information by performing an evaluation. Finally, an object may perform an action which is a prescription, creating a rule that constrains the future behaviour of the community. Prescriptions provide a flexible and powerful mechanism for changing the system's business rules at runtime, enabling its dynamic adaptation to respond to business changes and new needs.

Expressing accountability for actions allows the party responsible for the changes in the rules to be identified, which is something that fits well with the deontic nature of enterprise policies, because the party must be authorized in order to perform the prescription. These concepts can be used to express various governance frameworks. We can see these mechanisms at work in the PhoneMob example when a new contract is established with an organization fulfilling the role of Customer. The contract may be enacted by clicking on a button in some web page, but it is binding on the PhoneMob because the organization has performed a delegation to the Chief Information Officer, who is the party taking responsibility for the information system that acts as her agent in accepting the web interaction that enacts the agreement.

## 2.8 Quality of Service and Other Constraints

So far, the treatment of behaviour has concentrated on the sequence of tasks to be performed — the so-called functional aspects of the processes. However, we also need to be able to place constraints on various aspects of the quality of performance, such as how quickly things are done, how low the failure probability should be, or how good the security properties should be. This typically involves decorating the basic behaviour, which is a set of permitted event sequences, with conditions on what variations in performance are allowed.

For example, there will be policies that arise from a service level agreement between the PhoneMob and a VIP customer, such as obligations on the PhoneMob to observe response times for repairs and, in the case of violations, to provide compensation, such as arranging for replacement of a troublesome user handset.

This is a complex issue because there are many dependencies between the parties, and any quality guarantee asked from one community member is contingent on proper behaviour by others. For example, a requirement that the logistics provider shall deliver a shipment within 12 hours is contingent on the receiving party being available to take delivery before the end of the period. In general, any obligation placed on an object depends on guarantees of support given by its environment.

The details of how such quality constraints are expressed depend on the property being considered, and would take us beyond the scope of this book.
