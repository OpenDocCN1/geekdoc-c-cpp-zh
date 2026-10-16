# 20

# Diagnostics and Application Insights

# What’s In This Chapter?

+   - Simple Tracing with EventSource
+   - Advanced Tracing with EventSource
+   - Creating a Custom Trace Listener
+   - Using Application Insights

# Wrox.com Code Downloads for This Chapter

The wrox.com code downloads for this chapter are found at www.wrox.com/go/professionalcsharp6 on the Download Code tab. The code for this chapter is divided into the following major examples:

+   - SimpleEventSourceSample
+   - EventSourceSampleInheritance
+   - EventSourceSampleAnnotations
+   - ClientApp/MyApplicationEvents
+   - WinAppInsights

# Diagnostics Overview

As release cycles for applications become faster and faster, it’s becoming more and more important to learn how the application behaves while it’s running in production. What exceptions are occurring? Knowing what features are used is also of interest. Do users find the new feature of the app? How long do they stay in the page? To answer these questions, you need real-time information on the application.

This chapter explains how to get real-time information about your running application in order to identify any issues that it might have during production or to monitor resource usage to ensure that higher user loads can be accommodated. This is where the namespace System.Diagnostics.Tracing comes into play. This namespace offers classes for tracing using Event Tracing for Windows (ETW).

One way to deal with errors in your application, of course, is by throwing exceptions. However, an application might not fail with an exception, but it still doesn’t behave as expected. The application might be running well on most systems but have a problem on a few. On the live system, you can change the log by starting a trace collector and get detailed live information about what’s going on in the application. You can do this using ETW.