+   - Technology stack (execution environment) of the application
+   - The stack in which application data resides
+   - Features (such as Rete and flow rules or the ability to extend the BRMS)

As a rule of thumb, for best performance and integrated rule-editing experiences, we recommend using a rule engine that integrates deeply into the execution stack of business applications. Consequently, SAP provides two rule engines that seamlessly integrate with ABAP and Java stacks, respectively. For pure ABAP stack use cases, BRFplus shipped with SAP Business Suite is the best suited, whereas SAP NetWeaver BRM is best suited for pure Java use cases. For example, when a customer wants to leverage business rules in an SAP Business Suite application or add flexibility to an SAP Business Suite process, BRFplus would be the ideal choice. For customers creating composite applications and business processes using SAP NetWeaver CE, SAP NetWeaver BRM would be the ideal choice. The decision of which rules engine to use may go beyond technology stack considerations and hinge on the requirements of a particular use case.

In Figure 14.48, five usage recommendations are presented that can help in deciding which rule offering to use. On the horizontal axis there are the rule engines, SAP NetWeaver BRM and BRFplus, and on the vertical axis there are the SAP Business Suite core processes and composite applications (modeled processes).

![](bbox=[0.12, 0.68, 0.88, 0.9])

# Figure 14.48 Usage Recommendations for SAP Business Rules Offerings