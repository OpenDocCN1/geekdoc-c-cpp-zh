# E.7 THE COMMAND LINE DEBUGGER (CORDBG.EXE)

cordbg.exe is a command line debugger provided by the .NET Framework that allows you to debug .NET assemblies. It supports a number of flags for performing common debugging operations like addition and deletion of break points. Table E.3 lists some of the important command line arguments of cordbg.exe:

# Table E.3 Command Line arguments of cordbg.exe

| ARGUMENT | DESCRIPTION |
|---|---|
| b[reak] | Inserts a break point at the specified location. If no location is specified then the existing break points are displayed. |
| ca[tch] | Instructs the debugger to stop processing at the occurrence of the specified event. If no event is specified, then information pertaining to the existing event types is displayed. |
| Cont | Continues the execution of the program specified number of times. If no value is specified then the program execution is continued once. |
| del[ete] | Deletes the specified breakpoints. |
| ex[it] | Stops and exits the debugger. |
| h[elp] | Displays help information pertaining to cordbg.exe arguments. |

Before using the cordbg.exe tool for debugging an application one must generate the debugging information using the /debug option of the C# compiler. The /debug option creates a database file (.pdb) for storing the debugging information. This database file is automatically referenced by the cordbg.exe tool at the time of debugging the corresponding executable assembly. The .pdb file assumes the same name as the executable assembly.

Let us now go back to our Sample.cs application. Run the following command at the command prompt to generate its .pdb file:

```
csc @RspTest.rsp /debug
```

Now, type the following command to debug the application using cordbg.exe:

```
cordbg.exe Sample_Rsp.exe
```

Figure E.5 shows the output of the above command:

![](bbox=[0.18, 0.64, 0.835, 0.91])

Fig. E.5 Running cordbg.exe