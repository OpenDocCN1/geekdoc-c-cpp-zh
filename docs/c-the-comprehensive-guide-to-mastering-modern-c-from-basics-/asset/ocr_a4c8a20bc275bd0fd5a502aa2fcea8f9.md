gathered and defined as the set of tests to be executed. These are then all executed.

Each individual test can either pass (test is green) or fail (test is red). There may be noncritical warnings. If all tests were successful, this indicates overall success. A single failed test means a failure. It is not common to accept a certain number of individual errors.

Tests must run independently of each other. They must not rely on certain other tests having run before or not yet run. The framework can also run multiple tests simultaneously.

When executing a single test, the following happens:

+   1. The framework instantiates the test case containing the test.

+   2. Any existing setup function or method of the test case is called.

+   3. The framework calls the test using its test function.

+   4. The failure of an assertion or the unexpected exit of the test is noted and later reported as a fail.

+   5. If a teardown function or method exists, the framework calls it.

+   6. The test case is removed.

Note that this happens for every test: even if multiple tests are within a single test case, the test case is