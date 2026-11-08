To accommodate both, it is common to set up (at least) two suites of unit tests in your project:

+   - **Compile suite**  
+     Executed with every compile operation and should therefore run very quickly. As a rule of thumb, the test duration should be in the same order of magnitude as the compilation.
+   - **Commit suite**  
+     Performing a *commit* is completing a task by sending the source code back to the team. Once or twice a day is typical; in extreme cases, it might happen once a week. To ensure that everything still works as desired, you should allow this suite a bit more time to run—for example, a few minutes. However, it shouldn’t be much longer than that because if there are errors to fix, you need to be able to run the suite multiple times.

# 14.2  Frameworks

It is best to use a framework to write and execute your unit tests. There are different implementations for different languages, including C++. At the end of this chapter, I will introduce you to an example framework.

Certain terms have become established across frameworks. These are found as standard procedures grouped under the term *xUnit*. The following explanations are related in [Figure 14.3](#).

+   - **Test**  
+     A test is a special function that is called by the framework. Everything in unit testing revolves around tests, because a single test tests a single unit, a functionality. Within a test, you call the function to be tested and then write one or more assertions to verify the correct functionality.
+   - **Assertion**  
+     One assertion is performing a single check, typically the return value of the function to be tested. It always consists of a Boolean test, sometimes with a descriptive message upon failure. Often, side conditions are also checked with assertions. Some frameworks support two levels of assertions: warning and error. In the former, only a message is displayed if the assertion fails, while in the latter, the test fails. Here again, there are two variants: the test either continues or aborts.
+   - **Test case**  
+     Multiple tests are combined into a test case. Sometimes a test case contains only one test (as a test function), but often there are several. These then have something in common; for example, they require the same test environment or the same test fixture.