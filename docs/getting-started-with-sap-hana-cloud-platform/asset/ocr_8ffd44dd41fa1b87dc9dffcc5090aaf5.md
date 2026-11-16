SAP HCP instance) and pinpoint performance bottlenecks. In this section, we’ll observe how the SAP JVM Profiler can be used to identify segments of code that consume inordinate amounts of memory, I/O resources, and so on.

# Prerequisites for Using the SAP JVM Profiler

As the name suggests, the SAP JVM Profiler is built on top of SAP’s proprietary version of the JVM, called SAP JVM. Here, SAP went above and beyond the requirements of the default JVM specification to include first-class support for collecting performance traces from a running JVM instance.

Although SAP JVM is used by default in cloud-based SAP HCP instances, it’s technically possible to run the SAP HCP local runtime using any compliant JVM implementation. However, if you plan on running the SAP JVM Profiler on your local SAP HCP instance, then you must configure that instance to utilize the SAP JVM. For this reason (and others), we strongly recommend that you standardize around the SAP JVM so that you can keep your SAP HCP instances as consistent as possible. If you skipped over this step when you originally installed the SAP HCP SDK, then you can reconfigure your environment after the fact by using the steps described in Chapter 2, Section 2.3.3.

# Working with the SAP JVM Profiler

Similar to the debugger tool we explored in Section 3.4.1, the SAP JVM Profiler is a server-based function that can be controlled from within the Servers view in the Eclipse IDE. As you can see in Figure 3.23, we can control the SAP JVM Profiler by right-clicking on a server node and choosing the appropriate menu options (e.g., Restart in Profile). Once again, you’ll want to be careful not to disturb other users when profiling shared SAP HC instances.

Once the server node is (re)started in profile mode, we can launch the SAP JVM Profiler by opening up the Profiling perspective in Eclipse. By default, this perspective will bring up the VM EXPLORER view shown in Figure 3.24. From here, we can drill into the running profile by double-clicking on the record in the VM EXPLORER table.