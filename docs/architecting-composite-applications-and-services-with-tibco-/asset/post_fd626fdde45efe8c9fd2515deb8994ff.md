
![](img/b8d8132a583ad73d511c4c1bb92e2df7_98_0.png)

Figure 3-13: TIBCO Adapter for IBM i Deployment

## Mainframe and iSeries File Adapters

The TIBCO Adapter for Files z/OS (MVS) and TIBCO Adapter for Files (IBM i) provide off-mainframe access to files on their respective platforms. Files are accessible either in their entirety by block transfer (whole file) or by record for record-based processing.

Capabilities on the two platforms are slightly different. On the z/OS platform, applications can write to VSAM, sequential datasets (SEQs), generation dataset groups (GDGs), and partitioned datasets (PDSs). Applications can trigger the publishing of these same file types by sending a message. The adapter can also be configured to poll partitioned datasets (PDSs) and publish the files when they change. For the iSeries platform, the adapter can write and publish sequential (SEQ) files.

Deployment of both adapters is similar (Figure 3-14). The adapter itself resides on the mainframe, providing services via the TIBCO adapter protocol using either the Enterprise Message Service or Rendezvous transports. The TIBCO adapter protocol is supported by a wide range of products including ActiveMatrix Service Grid, ActiveMatrix Service Bus, and ActiveMatrix BusinessWorks.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_100_0.png)

Figure 3-15: BusinessConnect Deployment

Partners may connect directly with the engine using one of the supported B2B protocols or they may connect through a component running in a demilitarized zone (DMZ). The BusinessConnect DMZ Component enables connection via any of the supported B2B protocols. The BusinessConnect DMZ Servlet runs in an application server but only enables connection to a subset of the supported B2B protocols.

The BusinessConnect Interior Engine communicates with the enterprise's private processes using XML messages delivered by either Enterprise Message Service or Rendezvous transports. These messages are in BusinessConnect's aeRvMsg format. The TIBCO BusinessConnect™ Palette for BusinessWorks™ (supplied as a component of the BusinessConnect product) simplifies the use of this protocol.

## TIBCO Collaborative Information Manager

The TIBCO Collaborative Information Manager is designed to manage reference data (often referred to as master data) in the enterprise (Figure 3-16). Customer, partner, and product data generally fall into this category. This information is generally distributed across a number of systems, and the product makes it possible to manage this information in a consistent way.

![](img/b8d8132a583ad73d511c4c1bb92e2df7_101_0.png)

Figure 3-16: Simplified TIBCO Collaborative Information Manager Deployment

There are three major roles played by the information manager:

- 1. Provide a single consistent logical view of reference data and a single point for accessing this information.
- 2. Maintain the consistency of the data across multiple systems, detecting changes and managing the workflow updating other systems to maintain consistency.
- 3. When discrepancies cannot be automatically resolved, initiate and manage the human workflow required to investigate and resolve discrepancies.

Views of the managed information are available both through user (Web Client) interfaces and programmatic interfaces (SOAP, JMS, and File). These same interfaces can be used to inform the information manager of data changes in other systems as well as to update the data in those systems.

## Summary

There are a number of specialized TIBCO products that are often used in composite applications and services. These include Hawk, TIBCO Managed File Transfer products, a number of mainframe-related products, and BusinessConnect.

Hawk enables the rule-based monitoring of machines, components, and services in an environment. The Hawk Agent running in each machine environment uses rules to monitor the environment. It obtains detailed status information from components providing a Hawk Application Microagent Interface (AMI). When rule-defined conditions are recognized, the rule can initiate a variety of actions including executing command lines, interacting with microagents, and sending Hawk alerts, messages, and e-mails.

TIBCO Managed File Transfer product family controls the movement of files between systems. Files are transferred to and from Managed File Transfer servers that access local file systems. Internet servers enable the use of public protocols such as FTP for exchanging files with systems that do not have TIBCO Managed File Transfer components installed on them. File movement over communications links with high latency can be sped up by using the RocketStream Accelerator version of the products.

There are a number of mechanisms available for interacting with mainframes. Each mechanism provides a different assortment of interaction capabilities: program-to-program interaction, data access, and event recognition. For z/OS systems, options include the Substation ES, the ActiveMatrix BusinessWorks Plug-in for CICS, the TIBCO Adapter for Files z/OS (MVS), and the ActiveMatrix Adapter for Database. For the System i platform, options include the TIBCO Adapter for IBM i and the TIBCO Adapter for Files (IBM i).

BusinessConnect enables business-to-business interactions using a variety of protocols. It acts as an intermediary between these protocols and the enterprise's private business processes. It also provides non-repudiation capability, and it manages the registration and credentials for business partners.

TIBCO Collaborative Information Manager provides a consistent view of reference information distributed across multiple systems. It also provides the workflow necessary to maintain the consistency of that data as it gets updated in individual systems.

## Case Study: Nouveau Health Care

### Objectives

One of the challenges in writing about architecture and architecture patterns is to pick examples that are rich enough to motivate the discussion and realistic enough to represent real-world challenges while at the same time being simple enough to be readily explained.

The fictional Nouveau Health Care case study was created for this purpose. Its business processes, though simplified when compared with their real-world equivalent, are still complex enough to present most of the common design challenges found in their real-world counterparts. An important aspect of reality is that the processes and their corresponding solution implementations do not operate in isolation—they interact with one another and with other business processes as they would in the real world.

Different aspects of the Nouveau Health Care example are used throughout this architecture book series. This chapter provides a conceptual overview of the company and its business processes and then introduces the Payment Manager and its related business processes,

which are used to illustrate many of the points and design principles in this book.

## Nouveau Health Care Solution Architecture

Nouveau Health Care is a traditional health care insurance company. It sells health care insurance policies and covers claim payments with the revenue it collects from its premiums. It also administers the processing of claims.

There are factors that add to the complexity of Nouveau’s business. In some cases, the employers for whom Nouveau provides the health care benefits also provide the funds for paying the claims: Nouveau simply administers the policies. In other cases the administration of specialized services (vision and dental care) is farmed out to other companies. Both variations present some interesting design challenges.

## Nouveau Health Care Business Processes

Our use of Nouveau focuses on four of its business processes (Figure 4-1):

- 1. Validate Membership and its underlying Validate Membership Service
- 2. Manage Payments, which manages claim payments to health care service providers
- 3. Process Claim, and its initiator, Route Claim, which together handle the processing of insurance claims
- 4. Monitor Claim Processing, a process that monitors the execution of claim processing

The Validate Membership process is used by authorized parties (health care providers, employers, and members) to validate whether or not an individual was covered by the policy on a given date. This business process utilizes an underlying Validate Membership Service, which is also used by the Process Claim business process. Validate Membership is used as an example in the TIBCO® Architecture Fundamentals book.

The Manage Payments process manages the payments to health care service providers resulting from health care claims.¹ What makes
