You can use Process Manager to check whether the FSAnyCPU process is running, or you can use the sizeof operator to check the current IntPtr size. The 32-bit machine's IntPtr is 32-bit, so the sizeof operator returns 4 while the 64-bit machine will return 8. Listing 1-16 shows the execution result from

**LISTING 1-16** The sizeof IntPtr operator in FSI

```
> sizeof<System.IntPtr>;
val : int = 4
```

# FSI Directives

In addition to the #time directive, FSI offers several others:

+   * #help is used to display the help information about available directives.
* #I is used to add an assembly search path.
* #load is used to load a file, compile it, and run it.
* #quit is used to quit the current session. You will be prompted to press Enter to restart. This is how to restart a session from the keyboard.
* #r is used to reference an assembly.

The FSI is a great tool that can be used to run F# snippets of your code for test purposes. If your code is used to perform I/O operations, the FSI's default directory is the temp folder. Listing 1-17 shows how to get the current FSI folder and change its default folder.

**LISTING 1-17** Changing FSI's current folder

```
> System.Environment.CurrentDirectory;
val : string = "C:\Users\User\AppData\Local\Temp"
```

```
> System.Environment.CurrentDirectory <- "c:\\MyCode";
val : unit = ()
```

```
> System.Environment.CurrentDirectory;
val : string = "c:\\MyCode"
```

> **Note** After you reset the FSI session, the current folder will be set back to the temp folder.

![](bbox=[0.1, 0.806, 0.136, 0.846])