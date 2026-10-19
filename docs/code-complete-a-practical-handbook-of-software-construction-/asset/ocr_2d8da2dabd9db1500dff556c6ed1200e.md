+   - *Regression testing* is the repetition of previously executed test cases for the purpose of finding defects in software that previously passed the same set of tests.
+   - *System testing* is the execution of the software in its final configuration, including integration with other software and hardware systems. It tests for security, performance, resource loss, timing problems, and other issues that can’t be tested at lower levels of integration.

In this chapter, “testing” refers to testing by the developer, which typically consists of unit tests, component tests, and integration tests but can sometimes include regression tests and system tests. Numerous additional kinds of testing are performed by specialized test personnel and are rarely performed by developers, including beta tests, customer-acceptance tests, performance tests, configuration tests, platform tests, stress tests, usability tests, and so on. These kinds of testing are not discussed further in this chapter.

![](bbox=[0.14, 0.365, 0.208, 0.426])

Testing is usually broken into two broad categories: black-box testing and white-box (or glass-box) testing. “Black-box testing” refers to tests in which the tester cannot see the inner workings of the item being tested. This obviously does not apply when you test code that you have written! “White-box testing” refers to tests in which the tester is aware of the inner workings of the item being tested. This is the kind of testing that you as a developer use to test your own code. Both black-box and white-box testing have strengths and weaknesses; this chapter focuses on white-box testing because that’s the kind of testing that developers perform.

Some programmers use the terms “testing” and “debugging” interchangeably, but careful programmers distinguish between the two activities. Testing is a means of detecting errors. Debugging is a means of diagnosing and correcting the root causes of errors that have already been detected. This chapter deals exclusively with error detection. Error correction is discussed in detail in Chapter 23, “Debugging.”

The whole topic of testing is much larger than the subject of testing during construction. System testing, stress testing, black-box testing, and other topics for test specialists are discussed in the “Additional Resources” section at the end of the chapter.

# 22.1 Role of Developer Testing in Software Quality

> **Cross-Reference** For details on reviews, see Chapter 21, “Collaborative Construction.”

Testing is an important part of any software-quality program, and in many cases it’s the only part. This is unfortunate, because collaborative development practices in their various forms have been shown to find a higher percentage of errors than testing does, and they cost less than half as much per error found as testing does (Card 1987, Russell 1991, Kaplan 1995). Individual testing steps (unit test, component test, and integration test) typically find less than 50 percent of the errors present each. The combination of testing steps often finds less than 60 percent of the errors present (Jones 1998).