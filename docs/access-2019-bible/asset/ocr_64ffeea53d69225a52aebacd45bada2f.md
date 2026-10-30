# Chapter 22: Using Access Macros

➜ For more information on string concatenation using the ampersand (&), see Chapter 9.

The RemoveTempVar action removes a single temporary variable from memory—in this example, MyName. You can have only 255 temporary variables defined at one time. These variables stay in memory until you close the database, unless you remove them with RemoveTempVar or RemoveAllTempVars. It’s a good practice to remove temporary variables when you’re done using them.

> **CAUTION**
> 
> Using the RemoveAllTempVars action removes all temporary variables created with the SetTempVar action. Unless you’re sure you want to do this, use the RemoveTempVar action instead.

Temporary variables are global. Once you create a temporary variable, you can use it in VBA procedures, queries, macros, or object properties. For example, if you remove the RemoveTempVar action from mcrHelloWorldEnhanced, you can create a text box on a form and set its Control Source property as follows to display the name the user entered:

`= [TempVars]![MyName]`

# Using temporary variables to simplify macros

Using temporary variables, you can sometimes eliminate steps from a macro. You can get the form or report name from another control on a form. With a temporary variable, you eliminate the need for creating a structure of multiple OpenForm or OpenReport actions. You can also use more than one variable in a macro.

For this example, use frmReportMenuEnhanced (shown in Figure 22.15), which contains the same frmView shown in Figure 22.12 but adds a combo box (cboReport), which contains a list of reports to run. The Run Report command button executes mcrReportMenuEnhanced, which doesn’t use submacros to decide which report to open.

![](bbox=[0.19, 0.68, 0.47, 0.924])