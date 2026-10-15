![](bbox=[0.09, 0.09, 0.68, 0.48])

FIGURE 1-44

Within the rule set you see that there is a set of categories, each of which contains one or more rules. When expanded, next to each category and rule is a check box to indicate if that particular rule will be checked. By default, Visual Studio issue warnings if your code fails to meet the requirements associated with a rule. However, you can change the default — for example, by selecting an error status if a given rule fails. This enables you to have some rule violations act as compilation errors instead of warnings. Outside the scope of this chapter is the capability to actually identify within your source code those items that may be flagged by the code analyzer but that are valid exceptions to the rule being checked.

# Performance Tools

Every developer wants performance checks. Visual Studio provides dynamic code analysis, or performance, tools for your application. These tools are available from the Analyze menu, shown in Figure 1-45. Selecting the Performance Explorer from the menu shown in Figure 1-45 opens the window shown on the left side of the display in Figure 1-45. This window has a small bar and provides access to details and results of your performance testing.

A good way to get started with the performance tools is to select the first item from the Analyze menu, the Performance Wizard, shown in Figure 1-46. The performance tools provide four runtime environments to measure the performance of your application: CPU Sampling, Instrumentation, .NET Memory Allocation (Sampling), and Concurrency.

Sampling for performance testing is a non-intrusive method of checking your application performance. Essentially, Visual Studio starts your application normally, but behind the scenes it is interfaced into the system performance counters. As your application runs, the performance monitoring engine captures system performance, and when your application completes it provides reports describing that performance. Details about what your application was actually doing to cause a behavior isn’t available, but you can get a realistic idea of the impact on the system.