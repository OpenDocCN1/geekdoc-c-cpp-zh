appDomainManagerAssembly and appDomainManagerType elements. In addition, a native host could query for the ICLRControl interface and call this interface's SetAppDomainManagerType function, passing in the identity of the GAC-installed assembly and the name of the AppDomainManager-derived class.32

Now, let's talk about what an AppDomainManager-derived class can do. The purpose of the AppDomainManager-derived class is to allow a host to maintain control even when an add-in tries to create AppDomains of its own. When code in the process tries to create a new AppDomain, the AppDomainManager-derived object in that AppDomain can modify security and configuration settings. It can also decide to fail an AppDomain creation, or it can decide to return a reference to an existing AppDomain instead. When a new AppDomain is created, the CLR creates a new AppDomainManager-derived object in the AppDomain. This object can also modify configuration settings, how execution context is flowed between threads, and permissions granted to an assembly.

# Writing a Robust Host Application

A host can tell the CLR what actions to take when a failure occurs in managed code. Here are some examples (listed from least severe to most severe):

+   - The CLR can abort a thread if the thread is taking too long to execute and return a response. (I'll discuss this more in the next section.)
+   - The CLR can unload an AppDomain. This aborts all of the threads that are in the AppDomain and causes the problematic code to be unloaded.
+   - The CLR can be disabled. This stops any more managed code from executing in the process, but unmanaged code is still allowed to run.
+   - The CLR can exit the Windows process. This aborts all of the threads and unloads all of the AppDomains first so that cleanup operations occur, and then the process terminates.

The CLR can abort a thread or AppDomain gracefully or rudely. A graceful abort means that cleanup code executes. In other words, code in finally blocks runs, and objects have their Finalize methods executed. A rude abort means that cleanup code does not execute. In other words, code in finally blocks may not run, and objects may not have their Finalize methods executed. A graceful abort cannot abort a thread that is in a catch or finally block. However, a rude abort will abort a thread that is in a catch or finally block. Unfortunately, a thread that is in unmanaged code or in a constrained execution region (CER) cannot be aborted at all.

A host can set what is called an escalation policy, which tells the CLR how to deal with managed code failures. For example, SQL Server tells the CLR what to do should an unhandled exception be

32 It is also possible to configure an AppDomainManager by using environment variables and registry settings, but these mechanisms are more cumbersome than the methods mentioned in the text and should be avoided except for some testing scenarios.