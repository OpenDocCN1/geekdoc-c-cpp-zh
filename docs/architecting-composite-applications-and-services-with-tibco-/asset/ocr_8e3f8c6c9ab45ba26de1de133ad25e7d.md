additional choice as to which representation of Product you wish to use, as discussed in the previous section.

In case (b), the representation chosen for the product is just the orderedProduct field with the simple data type SKU that serves as an identifier for the product. Case (c) is even simpler—there is no representation of the product at all in the Sales Order Line Item.

# Designing an XML Schema

Given the choices available for representing entities and associations, how do you go about designing data structures? The process is relatively straightforward and involves the following steps:

+   1. Using the domain model, identify the entities and associations that need to be communicated.
+   2. For each entity and association, determine the type of representation that will be used.
+   3. Identify (if using common data models) or create the information model for the data structure.
+   4. Consider common data model implications and review and refine as appropriate.
+   5. Create the XML schema for the data structure.

When you want to reuse data types in the data structure, you'll probably iterate this design as you consider how the data types would be used in other data structures.

Let's look at an example of this process. Chapter 5 discussed a getOrder() operation whose response included the Sales Order, shipTo and billTo Address, and Sales Order Line Items (Figure 9-8).

Let's suppose now that you want to implement another operation, getOrderDetails(), that returns a richer set of information—more like the data set back in Figure 9-3. Furthermore, in doing so, you'd like to reuse data structures where possible. A sketch of this operation is shown in Figure 9-9. Your challenge is to define the Get Order Details Response.

These steps are illustrated in the following sections.