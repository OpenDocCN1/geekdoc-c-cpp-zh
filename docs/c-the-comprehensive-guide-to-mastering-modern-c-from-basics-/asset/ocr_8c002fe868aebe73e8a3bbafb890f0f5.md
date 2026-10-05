functional tests. Without this combination, you cannot maintain high code quality in the long run.

# ### Test-Driven Development

In the test-driven development (TDD) approach to programming, you first write the (unit) test and run it. Of course it fails, because you haven't written any program behind it yet. If it doesn't fail, you are doing something wrong because either your program already has the functionality (unlikely), or your test is useless and tests nothing. Only then do you extend your program with the functionality that the test checks. Do not program more than the test requires to avoid programming untested functionality.

Developers must first think about the interface of the function they want to write from an external perspective. In C++, you create the interface, for example, using an empty function. This is followed by the test, which fails, then by filling the function until the test passes.

This type of programming requires a lot of practice and discipline, but eventually it becomes second nature. You increase the quality of your code by having tests for everything and inevitably thinking more about the interfaces, because your test is your first user.

# 14.1.2 Unit Tests

In fact, there is not one definition of unit tests; there are several.