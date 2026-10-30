# FIGURE 22.19

mcrDivisionErrorHandling uses the OnError action to display a user-friendly error message and remove the temporary variables.

![](bbox=[0.15, 0.24, 0.85, 0.62])

# NOTE

There's no Resume functionality in macro error handling. If you want to run additional code after the error-handling actions, you must use the RunMacro action in the error-handling submacro to run another macro or place the actions in the error handler.

The RunMacro action also appears after the MessageBox action in the main section of the macro. Because you're using submacros, the macro stops after it reaches the ErrorHandler submacro. In order to force the cleanup of the temporary variables, use the RunMacro action to run the Cleanup submacro. Otherwise, you'd have to put the RemoveTempVar actions in the main section and in the ErrorHandler section of the macro.

# The MacroError object

The MacroError object contains information about the last macro error that occurred. It retains this information until a new error occurs or you clear it with the ClearMacroError action. This object contains a number of read-only properties you can access from the macro itself or from VBA. These properties are as follows:

+   - ActionName: This is the name of the macro action that was running when the error occurred.