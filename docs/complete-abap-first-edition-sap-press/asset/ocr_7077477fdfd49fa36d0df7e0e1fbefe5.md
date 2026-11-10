# Customer Developments

If you can’t find a suitable enhancement option, don’t wish to modify a standard SAP program, or can’t find a suitable standard SAP object that fulfills your company-specific requirement, you can create your own repository objects (such as tables, programs, transactions, etc.). All customer developments normally take place in a customer namespace, meaning that the names of all objects created by a customer should start with Y or Z.

For example, let’s say your company has to implement a new business solution for a specific region due to a change in local laws of that region and there is no standard SAP solution that meets the requirement. In such scenarios, you can develop your custom applications to implement the business requirements. These custom applications will be in a customer namespace and will coexist with standard SAP applications.

Figure 1.3 depicts the customization overview. As you can see, modifications fall under the SAP namespace, because modifications change the standard SAP program directly, whereas enhancements and customer developments fall under the customer namespace and are immune to being changed during upgrades.

![](bbox=[0.142, 0.503, 0.681, 0.841])

**Figure 1.3** Customization Overview