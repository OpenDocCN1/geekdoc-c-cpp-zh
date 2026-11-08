+   8. TITLE1 is defined before the DATA step that will call the routine; however, this title will not be available to the macro executed by the PRNTCRIT routine.

+   9. The PRNTCRIT routine is called using three variables from the ADVRPT.DSNCONTROL data set. The variables in the routine call must be in the same order as they are defined ❷. The PRNTCRIT routine is called for each observation on the incoming data set. The routine calls and executes the macro %PRINTIT. Unlike the CALL EXECUTE routine, which pushes the macro call to a stack, %PRINTIT will be executed immediately.

+   10. The TITLE1 will be honored, but the TITLE2 will be undefined.

Because functions and routines are compiled, we cannot use a macro call directly within the function definition. If we had attempted to specify the macro call directly as shown here, %PRINTIT would have executed while the PRNTCRIT routine was being compiled. Macro calls

```
```sas
proc fcmp outlib=advrpt.functions.utilities;
subroutine prntcrit(dsn$, kvar $,cvar $);
    %printit(dsn,kvar,cvar);
. . . . . .
```
```

such as this one would be used to generate routine or function code. Macros that are to be executed during function execution should be specified

with the RUN_MACRO function as was shown above.

# MORE INFORMATION

The DQUOTE function is introduced in Section 3.6.7.

# SEE ALSO

Chapter 8 in *Carpenter’s Complete Guide to the SAS® Macro Language, 2nd Edition* (Carpenter, 2004) discusses the use of macros and macro variables within the context of compiled code.

# 15.2.4 Viewing Function Definitions

User-defined functions do not appear in the SASHELP.VFUNC view or in the DICTIONARY.FUNCTIONS table. However, under Windows you can see both the list of available functions and their attributes through the use of the FCMP Function Editor.

To start this editor, go to SOLUTIONS → ANALYSIS → FCMP FUNCTION EDITOR. The list of available data sets and the functions that they contain is shown in the left pane. Selecting a function brings up the editor dialog box, which allows you to see the details of the function’s definition.