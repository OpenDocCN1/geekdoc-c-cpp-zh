
### Figure 19.14

Adding a data source modifies the testing code. With a data source, the test class is annotated with the DeploymentItem attribute (if a CSV or XML file is used), and with DataSource and DataBinding attributes:

```
[DeploymentItem("webandloadtestproject\\EmailTests.csv", "webandloadtestproject")]
[DataSource("EmailDataSource", "Microsoft.VisualStudio.TestTools.DataSource.CSV", "|DataDirectory|\\webandloadtestproject\\EmailTests.csv", Microsoft.VisualStudio.TestTools.WebTesting.DataBindingAccessMethod.Sequential, Microsoft.VisualStudio.TestTools.WebTesting.DataBindingSelectMethod.BoundColumns, "EmailTests#csv")]
[DataBinding("EmailDataSource","EmailTests#csv","sample1@test#com", "EmailDataSource.EmailTests#csv.sample1@test#com")]
public class NavigateAndRegister1: WebTest
{
    // etc.
}
```

Now, in the code the data source can be accessed using the Context property of the WebTest that returns a WebTestContext to access the required data source via an index:

### New Test Data Source Wizard

### Select the type of data source

Data source name: DataSource1

Data source type:
- Database
- CSV File
- XML File

Please select the type of data that will be the basis for this data source.

< Previous   Next >   Finish   Cancel

### Figure 19.16

### Web Load Test

Using Web Load Tests, you can simulate a high load on the web application. For a really high load one test server is not enough; you can use a list of test servers. With Visual Studio 2015, you can directly use the infrastructure of Microsoft Azure and select a Cloud-based Load Test as shown in Figure 19.17.

![](img/3d365b72b289213a91ade7eb366b8f35_728_0.png)

### Figure 19.17

You can create a load test by adding a new item Web Load Test to the WebAndLoadTestProject project. This starts a wizard where you can do the following:

- Define a constant load or a load that increases over time (see Figure 19.18)
- Establish a test mix model based on the number of tests or the number of virtual users
- Add tests to the load and define which test should run what percentage compared to the other tests
- Specify a network mix to simulate fast and slow networks (what’s the result for a user with a slow network if the server is occupied by clients with fast networks?)
- Determine a browser mix to test with Internet Explorer, Chrome, Firefox, and other browsers
- Establish run settings to run for the time to run the test

![](img/3d365b72b289213a91ade7eb366b8f35_729_0.png)

### Figure 19.18

### Summary

In this chapter, you’ve seen the most important aspects about testing applications: creating unit tests, coded UI tests, and Web tests.

Visual Studio offers a Test Explorer to run unit tests, no matter whether they have been created using MSTest or xUnit. xUnit has the advantage of supporting .NET Core. This chapter also showed you triple A in action: Arrange, Act, and Assert.

With coded UI tests, you’ve seen how to create recordings and adapt the recordings to modify the UI testing code as needed.

With web applications, you’ve seen how to create a Web test to send requests to the server. You also found out how to change the requests.

Although testing helps with fixing issues with applications before they are deployed, Chapter 20, “Diagnostics and Application Insights,” helps you fix applications that are running.

## 20 Diagnostics and Application Insights

### What’s In This Chapter?

- Simple Tracing with EventSource
- Advanced Tracing with EventSource
- Creating a Custom Trace Listener
- Using Application Insights

### Wrox.com Code Downloads for This Chapter

The wrox.com code downloads for this chapter are found at www.wrox.com/go/professionalcsharp6 on the Download Code tab. The code for this chapter is divided into the following major examples:

- SimpleEventSourceSample
- EventSourceSampleInheritance
- EventSourceSampleAnnotations
- ClientApp/MyApplicationEvents
- WinAppInsights

### Diagnostics Overview

As release cycles for applications become faster and faster, it’s becoming more and more important to learn how the application behaves while it’s running in production. What exceptions are occurring? Knowing what features are used is also of interest. Do users find the new feature of the app? How long do they stay in the page? To answer these questions, you need real-time information on the application.

This chapter explains how to get real-time information about your running application in order to identify any issues that it might have during production or to monitor resource usage to ensure that higher user loads can be accommodated. This is where the namespace System.Diagnostics.Tracing comes into play. This namespace offers classes for tracing using Event Tracing for Windows (ETW).

One way to deal with errors in your application, of course, is by throwing exceptions. However, an application might not fail with an exception, but it still doesn’t behave as expected. The application might be running well on most systems but have a problem on a few. On the live system, you can change the log by starting a trace collector and get detailed live information about what’s going on in the application. You can do this using ETW.

If there are problems with applications, the system administrator needs to be informed. The Event Viewer is a commonly used tool that not only the system administrator should be aware of but also the software developer. With the Event Viewer, you can both interactively monitor problems with applications and can add subscriptions to be informed about specific events that happen. ETW enables you to write information about the application.

Application Insights is a Microsoft Azure cloud service that enables you to monitor apps in the cloud. With just a few lines of code, you can get detailed information about how the application or service is used.

This chapter explains these facilities and demonstrates how you can use them for your applications.

> **NOTE** The System.Diagnostics namespace also offers other classes for tracing, such as Trace and TraceSource. These classes have been used in previous versions of .NET. This chapter goes into only the newest technology for tracing: EventSource. You can read Professional C# 5.0 and .NET 4.5.1 for the older tracing types.

### Tracing with EventSource

Tracing enables you to see informational messages about the running application. To get information about a running application, you can start the application in the debugger. During debugging, you can walk through the application step by step and set breakpoints at specific lines and when you reach specific conditions. The problem with debugging is that a program with release code can behave differently from a program with debug code. For example, while the program is stopping at a breakpoint, other threads of the application are suspended as well. Also, with a release build, the compiler-generated output is optimized and, thus, different effects can occur. With optimized release code, garbage collection is much more aggressive than with debug code. The order of calls within a method can be changed, and some methods can be removed completely and be called in place. There is a need to have runtime information from the release build of a program as well. Trace messages are written with both debug and release code.

A scenario showing how tracing helps is described here. After an application is deployed, it runs on one system without problems, whereas on another system intermittent problems occur. When you enable verbose tracing, the system with the problems gives you detailed information about what’s happening inside the application. The system that is running without problems has tracing configured just for error messages redirected to the Windows event log system. Critical errors are seen by the system administrator. The overhead of tracing is very small because you configure a trace level only when needed.
