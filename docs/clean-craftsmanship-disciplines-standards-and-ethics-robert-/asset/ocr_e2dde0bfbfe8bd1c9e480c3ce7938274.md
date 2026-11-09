The first of the disciplines, of course, is tests. Tests, tests, tests, tests, and more tests. To safely and reliably refactor your code, you need a test suite that you trust with your life. You need tests.

# ## Quick Tests

The tests also need to be quick. Refactoring just doesn't work well if your tests take hours (or even minutes) to run.

In large systems, no matter how hard you try to reduce test time, it's hard to reduce it to less than a few minutes. For this reason, I like to organize my test suite such that I can quickly and easily run *the relevant subset* of tests that check the part of the code I am refactoring at the moment. This usually allows me to reduce the test time from minutes to sub-seconds. I run the whole suite once every hour or so just to make sure no bugs leaked out.

# ## Break Deep One-to-One Correspondences

Creating a test structure that allows relevant subsets to be run means that, at the level of modules and components, the design of your tests will mirror the design of your code. There will likely be a one-to-one correspondence between your high-level test modules and your high-level production code modules.

As we learned in the previous section, deep one-to-one correspondences between tests and code lead to fragile tests.

The speed benefit of being able to run relevant subsets of tests is much greater than the cost of one-to-one coupling *at that level*. But in order to prevent fragile tests, we don't want the one-to-one correspondence to continue. So, below the level of modules and components, we purposely break that one-to-one correspondence.

# ## Refactor Continuously