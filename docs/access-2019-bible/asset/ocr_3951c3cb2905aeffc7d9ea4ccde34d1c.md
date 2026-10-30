# FIGURE 22.24

The newly converted module.

![](bbox=[0.185, 0.173, 0.887, 0.432])

When you specify that you want Access to include error processing for the conversion, Access automatically inserts the On Error statement as the first command in the procedure. The On Error statement tells Access to branch to other statements that display an appropriate message and then exit the function.

The statement beginning with TempVars.Add is the actual code that Access created from the macro. Each line of the macro is converted into a line of VBA code, including the TempVars object, the Beep method, and the MsgBox function.

If you’re new to VBA and want to learn code, a good starting point is converting your macros to modules. Just save your macros and modules, and then look at the VBA code to become familiar with the syntax. The macro features in Access 2019 make it harder to decide whether to use macros or VBA.