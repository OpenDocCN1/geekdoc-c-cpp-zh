# # 14.2 Frameworks

It is best to use a framework to write and execute your unit tests. There are different implementations for different languages, including C++. At the end of this chapter, I will introduce you to an example framework.

Certain tests have become established across frameworks. These are found as standard procedures grouped under the term xUnit. The following explanations are related in Figure 14.3:

+   * Test
  A test is a special function that is called by the framework. Everything revolves around tests, because a single test tests a single unit, a functionality. Within a test, you call the function to be tested and then write one or more assertions to verify the correct functionality.

+   * Assertion
  One assertion is performing a single check, typically the return value of the function to be tested. It always consists of a Boolean test, sometimes with a descriptive message upon failure. Often, side conditions are also checked with assertions. Some frameworks support two levels of assertions: warning and error. In the former, only a message is displayed if the assertion fails, while in the latter, the test fails. Here again, there are two variants: the test either continues or aborts.