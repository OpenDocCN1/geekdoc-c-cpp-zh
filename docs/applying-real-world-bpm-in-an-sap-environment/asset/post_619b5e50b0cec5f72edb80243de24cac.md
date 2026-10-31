
![](img/30a88f75957f887ca511028d178ca5c7_475_0.png)

**Figure 14.24** New Business Analyst Perspective

Process performance reporting and monitoring has been introduced as model artifacts to support gaining better process performance insight and thus help improve process quality.

A browser-based rules manager has been introduced to enable process analysts to directly modify business rules without the need to use the full developer experience. In addition, the expressiveness of rules has been enhanced by the addition of common definitions, effective dates for rules, and overrides.

## 14.2.2 Process Developer Experience

In SAP NetWeaver BPM 7.2 the various stages of composite process design are more effectively supported, starting from rapid prototyping with the ability to build and deploy incomplete process models by inclusion of default tasks and mock services targeted at increasing developer productivity. As illustrated in Figure 14.25 and Figure 14.26, the following improvements have been included:

![](img/30a88f75957f887ca511028d178ca5c7_478_0.png)

**Figure 14.27** Intermediate Message Events Support Correlation of Event Messages to Running Process Instances

## 14.2.5 Interoperability with Other Task User Interfaces

Developers create specialized UIs for human tasks defined as part of an SAP NetWeaver BPM process. In the first version of SAP NetWeaver BPM, these UIs were developed using SAP's model-driven Java UI technology, Web Dynpro for Java. In SAP NetWeaver BPM 7.2, task UIs created with SAP NetWeaver Visual Composer are also supported. SAP NetWeaver Visual Composer is a powerful design tool that supports graphical, model-driven definition of UIs rather than coding. Although simple enough to use for some power business users, SAP NetWeaver

Visual Composer provides rich connections to SAP applications. Both UI technologies can be used directly from the process context of the BPM model, and with the help of a wizard, the UIs can be generated automatically, which increases developer productivity considerably, particularly when complex data structures are included in the process context.

SAP NetWeaver BPM 7.2 also offers support for Adobe offline forms, allowing task participants to interact with business processes offline via email. Tightly integrated support for offline forms extends the reach of SAP NetWeaver BPM to a new class of task workers, including sales professionals who spend much of their workday in the field.

SAP NetWeaver BPM is part of SAP NetWeaver Composition Environment (CE). For more details about how to leverage the capabilities of SAP NetWeaver CE, please go to Section 14.1.

## 14.3 Handling Decisions and Business Rules in a BPM Approach

In this chapter we explore how managing decisions and business processes as peers creates simpler and more agile processes and more flexible business applications. Externalizing operational decisions from process designs and applying SAP’s business rules offerings to effectively manage the logic behind those decisions improves visibility, gives the business the power to maintain policies themselves, builds in a capacity for change, and helps ensure business-IT alignment. The key is to apply focus on the decisions within processes in addition to the processes themselves. This makes these decisions and the business rules within them explicit and provides a basis for line-of-business owners to assert control over these decisions.

Many business processes are about arriving at decisions. They define the collaboration and collection of information and documentation required to make a decision. Decisions are also at the heart of many operational business processes. To execute an enrollment process, we must know if someone is eligible for the product. To sell a complex, highly configured product to a company, we must know if the product configuration is valid and what the price would be for that customer. To process a claim or a tax return, we must be able to decide if it should be fast-tracked, reviewed, or investigated for fraud. We must make these potentially complex decisions every time we execute the process. Other operational processes involve

Take the process shown in Figure 14.28, for instance. In this case the process has been designed without an explicit decision, and a series of branches has been used to select from the various options — the activities that process an applicant differently according to the risk of the applicant. One can easily see how the process might have started with a single gateway, perhaps one based on age, and gradually become more complex as more specificity was added over time. Even with a few simple checks this process is already becoming messy and hard to follow.

![](img/30a88f75957f887ca511028d178ca5c7_481_0.png)

**Figure 14.28** Complexity Resulting from an Implicit Decision

Contrast this with Figure 14.29. In this case the process has an explicit decision identified — an activity for deciding how risky an applicant is. The process is simpler, with a single gateway, and it will not need changing unless we decide to add a fourth risk category with associated risk-specific processing. Any changes we decide to make regarding how we determine the riskiness of the applicant take place within the decision-making activity and do not impact the process design. If a government were to release new rules forbidding age to be used, for example, the process would not have to change, because we could simply update the decision-making activity to reflect this new regulation. We have separated these concerns, allowing us to change them independently, and we have simplified the process dramatically.

bonuses, will be limited. Externalizing the loyalty reward decisions as an explicit component and using business rules to manage its behavior (in this case as a BRF-plus function in SAP CRM Loyalty Management) will address this.

### Increased Capacity for Change

Hard-coded decisions and manual decision-making both reduce your capacity for change. Hard-to-change systems, those requiring significant IT resources to be devoted to changing programmed logic, cannot be changed quickly, and many IT organizations are so backlogged that only business-critical changes can be considered. If you rely on manual decision-making, you are not dependent on bottlenecked IT resources. However, updating policy manuals and retraining staff are time-consuming and expensive. Ensuring that changes to decision-making are promulgated throughout the organization and that the decisions are made consistently can be a massive and expensive undertaking. Inconsistent decisions resulting from partially implemented changes to manual decision-making can lead to fines, bad customer service, and unnecessary losses.

To be responsive to change, you need to keep key business decision-making visible, understandable, and changeable. Critical decisions cannot be buried in software code or company manuals where the business has zero visibility into the behavior they represent. Explicitly identifying decisions and describing the logic behind them allows this logic to be managed separately from processes and systems, increasing your capacity for change.

Business users like business process management software because it allows them to change their workflow easily; it increases the capacity for change of the process. Managing decisions further increases this capacity because business changes often involve updates to business decisions — to pricing, eligibility, or risk assessment decisions, for example. These decisions are often the most dynamic part of a process, the part that changes most often.

For instance, a company's pricing rules are likely to change far more often than its order-to-cash process. Adding an explicit pricing decision that business users can control allows them to make pricing changes without impacting the process. They can manage the process and the decision separately.

### Improved Alignment

Given the importance of systems and processes to today's organization, business and IT professionals must be aligned. The IT department plays a critical role in
