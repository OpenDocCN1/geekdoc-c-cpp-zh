The process begins with knowing and thoroughly understanding the target being tested. The process then proceeds with the following steps:

+   - Specify the target's inputs and outputs.
+   - Develop the input test case vector suite(s).
+   - Identify the target's expected outputs for each test case.
+   - Execute the tests.
+   - Track and collect test results.
+   - Compare the results with the corresponding expected results.
+   - Identify and correct any identified problems.

**black box**
**gray box**
**white box**
Test suites can be classified into three categories, black box, gray box, and white box testing, based upon foreknowledge of the target's internals. Black box testing assumes no knowledge of the target's internal design, white box assumes full knowledge, and gray box reflects partial knowledge.

# 8.23.1.3.1 BLACK BOX TEST

Black box tests assume no knowledge of system or subsystem internals. The target is tested from a purely external perspective and is, therefore, data driven. The test cases are generated and applied. Test failure aborts the test and the fault(s) should be identified and fixed. Testing resumes from the beginning. Black box testing requires that module interfaces be clearly defined. A major weakness with such tests is that the tests can be exhaustive and, thus, very time consuming. Because of the lack of knowledge of the system or subsystem internals, black box tests may miss dead code or certain paths through the code.

# 8.23.1.3.2 WHITE BOX TESTING

White box tests assume perfect knowledge of system or subsystem internal implementation. Testing further requires that module interfaces be clearly defined. Tests are logic driven and the target is tested from an internal point of view. Test cases are generated and applied. The tests are designed to exercise every internal path and code segment. Test failure aborts the test, and the fault(s) are identified and fixed. Testing then resumes from the beginning.

# 8.23.1.3.3 GRAY BOX TESTING

Gray box tests are a mix of white and black box testing. The method applies when the system utilizes modules we did not design, such as complex large or very large integrated circuits, gate arrays, or library modules.

# 8.23.1.4 Fourth Steps

Document, date, and assign a version number for each change following release of the product and ensure at each boot that the version numbers of all modules are consistent with those expected to be in the system.

Testing the system software once, then deploying without a revisit because it has been tested is a weak defensive strategy. That said, security is never perfect; what was put together by humans can be broken by humans. Operators and other users are routinely looking for new ways to work around or bypass the “annoying” access requirements.

The systems, technologies, repairs, users, data, potential updates over time can often appear routine. With such changes, new risks can be and often are introduced. To mitigate