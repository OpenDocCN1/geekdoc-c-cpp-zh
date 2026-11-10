but also help you understand and maintain enhancements implemented using old techniques.

Many companies are reluctant to convert their old code to new technology; it requires a lot of effort without necessarily providing any new benefits over the old implementation. SAP recommends that we use the latest available technology for any new implementations but doesn't force customers to convert their existing implementations.

The enhancement concept works on the basis that SAP can leave an opening in the code while developing the standard SAP program, and customers can add their code in these openings (*hooks*) to enhance the application. This concept depends heavily on the developer of the standard SAP program anticipating where customers might want to add their code in the standard SAP program and providing a hook accordingly.

In some situations, suitable hooks may not be available for you to enhance the application. For enhancements to meet customer requirements, the hook should be provided at the right place in the program flow and provide access to the data that a customer wants to change.

For example, when a user creates a sales order in a standard SAP application, the application doesn't put any restriction on item quantity. However, if your organization deals with wholesale retail and you want to put a restriction on the minimum quantity that can be ordered for each item, you need to validate the order quantity for the item and allow only bulk orders over a specified order quantity to be saved.

To enhance the standard SAP application to implement this custom requirement, you need a hook that's triggered before the document is saved and provides access to the item quantity for validation. If the developer of the standard SAP application has provided a hook *after* the document is saved, it's of no use for your requirement.

When studying if a particular enhancement meets our requirements, we look at when the enhancement is triggered in the standard SAP program flow and what data is available to manipulate. If we can't find any enhancements for a standard SAP program that meet our requirements, we need to explore other options for customizing the application, such as modifications or new developments. This