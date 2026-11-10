Once you turn on the trace, record the transaction and turn off the trace to display the results. The results screen shows the trace list of all the statements that were executed between turning on and turning off the trace. From the default view, as shown in Figure 21.22, you can navigate to different views, as shown in Figure 21.21. Each view provides different information about the database access, allowing you to perform an in-depth analysis.

![](bbox=[0.148, 0.243, 0.856, 0.414])

**Figure 21.22** Display Trace

In the default view shown in Figure 21.22, you can double-click any cell to open the respective view. For example, double-clicking a specific statement in the Statement column will open the SQL statement's trace record; double-clicking an object name in the Object Name column will show information about the object, and so on.

The Duration column shows the time taken to execute the statement. It takes into account not only the time taken to perform the action in the database, but also the time taken by the network between the database interface and the database.

As shown in Figure 21.21, there are a number of selectable views to choose from:

+   - **Structure-Identical Statements**
+     This view allows you to check any redundant statements that were executed.
+   - **Value-Identical Statements**
+     This view allows you to check any statements that return identical values.
+   - **Access to Tables**
+     This view provides the cumulative time spent on each table for different operations.