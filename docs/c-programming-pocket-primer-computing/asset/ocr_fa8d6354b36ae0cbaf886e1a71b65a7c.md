checks the timestamp of a file and its dependencies in order to determine whether a target must be invoked. In addition, when dependencies are checked, updates are performed recursively.

For example, if a C source code file has a timestamp that is more recent than its corresponding executable, then the associated target in the makefile is invoked, and the associated commands are executed.

In many cases the purpose of the makefile is to create an executable, and the associated target is often the first target in the makefile. For example, if `FindMain2` is the first target in a makefile, then make will execute the commands for the target `FindMain2`.

> **NOTE** By default "make" always runs the commands from the first target in the makefile, but not any of the commands in other targets.

If you do not specify the "-o" switch the compiler will create the default executable whose name is `a.out`.

+   In general terms, a makefile contains one or more entries, where each entry consists of the following:
+   
+   - a target (usually a file)
+   - its dependencies (the files that the target depends on)
+   - the commands to invoke (based on the target and dependencies)

Keep in mind that dependencies are transitive. For example, if A depends on B and B depends on C, then A depends on C. Examine your C programs to determine the dependencies for each file and then add the appropriate target to your makefile.