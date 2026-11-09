+   Generations: Improving Performance. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .513
+   Garbage Collection Triggers . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .519
+   Large Objects . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .519
+   Garbage Collection Modes. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .520
+   Forcing Garbage Collections . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .522
+   Monitoring Your Application's Memory Usage . . . . . . . . . . . . . . . . . . . . . .524
+   Working with Types Requiring Special Cleanup . . . . . . . . . . . . . . . . . . . . .525
+   Using a Type That Wraps a Native Resource. . . . . . . . . . . . . . . . . . . . . . .532
+   An Interesting Dependency Issue . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .537
+   Other GC Features for Use with Native Resources . . . . . . . . . . . . . . . . . . .538
+   Finalization Internals . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .542
+   Monitoring and Controlling the Lifetime of Objects Manually . . . . . . . . . . . .545

# **Chapter 22 CLR Hosting and AppDomains** **553**

+   CLR Hosting . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .554
+   AppDomains . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .556
+   Accessing Objects Across AppDomain Boundaries . . . . . . . . . . . . . . . . . . . . .559
+   AppDomain Unloading . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .570
+   AppDomain Monitoring . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .571
+   AppDomain First-Chance Exception Notifications . . . . . . . . . . . . . . . . . . . .573
+   How Hosts Use AppDomains . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .574
+   Executable Applications . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .574
+   Microsoft Silverlight Rich Internet Applications . . . . . . . . . . . . . . . . . . . .574
+   Microsoft ASP.NET and XML Web Services Applications . . . . . . . . . . . . . . .575
+   Microsoft SQL Server. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .575
+   Your Own Imagination . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .576
+   Advanced Host Control . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .576
+   Managing the CLR by Using Managed Code . . . . . . . . . . . . . . . . . . . . . . . .576
+   Writing a Robust Host Application . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .577
+   How a Host Gets Its Thread Back . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .578