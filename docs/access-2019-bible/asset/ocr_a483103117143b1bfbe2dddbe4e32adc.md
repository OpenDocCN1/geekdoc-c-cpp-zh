# Using conditional watches

Although watching variables in the Locals window or Watches window can be entertaining, you can spend a lot of unproductive time hoping to see something unexpected happen. You'll probably find it much more efficient to set a conditional watch on a variable, and instruct the VBA engine to break when the condition you've established is met.

The Add Watch dialog box (see Figure 27.17) accepts a Boolean (True or False) expression, such as rs.Fields("OrderID").Value=10251 in the text box near the top. You specify where in the application (which procedures and which modules) the expression is applied, and you tell Access what you want the VBA engine to do when the expression is evaluated. For our purposes, we want execution to break when the loop reaches a record whose OrderID field is equal to 10251—that is, when the preceding expression is True.

# FIGURE 27.17

A conditional watch halts execution when the expression rs.Fields("OrderID").Value=10251 is True.

![](bbox=[0.24, 0.55, 0.62, 0.75])

Running the FillRecordset1 procedure in the modSQLStatement module with this watch set will cause the code to stop on the Loop statement. At this point, you can inspect the other values in the recordset via the Locals window or write some statements in the Immediate window to investigate a problem.

The conditional watches you set up through the Add Watch dialog box are added to the Watches window. The watch expression appears in the Watches window's Expression column.

You can use conditional watches in other ways, too, such as using compound conditions (X = True And Y = False), and forcing a break whenever a value changes from the value set in the Expression text box. The small example illustrated in Figure 27.17 only hints at the capabilities possible with conditional watches.