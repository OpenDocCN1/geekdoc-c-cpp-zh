# Part III: Working with Access Queries

+   ▪ **Validation rule set to anything:** If a field in the destination table has a validation rule and you break the rule with your append query, your append query will fail. For example, if you have a validation rule for the Cost field in your destination table set to `>0`, you can’t append records with a quantity less than or equal to zero.

Luckily, Access will clearly warn you if you’re about to cause any of these errors. Figure 10.15 demonstrates this warning message, which tells you that you can’t append all the records due to errors. It also tells you exactly how many records won’t be appended because of each error. In this case, 5,979 records won’t be appended because of key violations. You have the option of clicking Yes or No. If you click Yes, the warning is ignored and all records are appended, minus the records with the errors. If you click No, the query will be canceled, which means that no records will be appended.

# FIGURE 10.15

The warning message tells you that you’ll lose records during the append process.

![](bbox=[0.167, 0.388, 0.866, 0.504])

> **CAUTION**
> 
> Keep in mind that like all other action queries, you won’t be able to undo your append query once you’ve pulled the trigger.

> **TIP**
> 
> If you can identify the records you recently appended in your destination table, you could technically undo your append action simply by deleting the newly appended records. This would be obviously contingent upon your providing yourself with a method of identifying appended records. For example, you could create a field that contains some code or tag that identifies the appended records. This code can be anything from a date to a simple character.

Let’s say the marketing department tells you that they made a mistake—they actually need all the sales history for the 2012 fiscal year. So, they need periods 201201 through 201205 added back to the SalesHistory report. An append query is in order.

In order to get them what they need, follow these steps:

+   1. **Create a query in the Query Design view that looks similar to the one shown in Figure 10.16.**
+   2. **Select the Design tab of the Ribbon, and then click the Append button.** The Append dialog box (shown in Figure 10.17) appears.