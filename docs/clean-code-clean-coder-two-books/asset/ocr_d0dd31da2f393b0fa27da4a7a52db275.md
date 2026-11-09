there are conditions that have not been explored by the tests or calculations that have not been validated.

# **T2: _Use a Coverage Tool!_**

Coverage tools reports gaps in your testing strategy. They make it easy to find modules, classes, and functions that are insufficiently tested. Most IDEs give you a visual indication, marking lines that are covered in green and those that are uncovered in red. This makes it quick and easy to find if or catch statements whose bodies haven’t been checked.

# **T3: _Don’t Skip Trivial Tests_**

They are easy to write and their documentary value is higher than the cost to produce them.

# **T4: _An Ignored Test Is a Question about an Ambiguity_**

Sometimes we are uncertain about a behavioral detail because the requirements are unclear. We can express our question about the requirements as a test that is commented out, or as a test that annotated with `@Ignore`. Which you choose depends upon whether the ambiguity is about something that would compile or not.

# **T5: _Test Boundary Conditions_**

Take special care to test boundary conditions. We often get the middle of an algorithm right but misjudge the boundaries.

# **T6: _Exhaustively Test Near Bugs_**

Bugs tend to congregate. When you find a bug in a function, it is wise to do an exhaustive test of that function. You’ll probably find that the bug was not alone.

# **T7: _Patterns of Failure Are Revealing_**

Sometimes you can diagnose a problem by finding patterns in the way the test cases fail. This is another argument for making the test cases as complete as possible. Complete test cases, ordered in a reasonable way, expose patterns.