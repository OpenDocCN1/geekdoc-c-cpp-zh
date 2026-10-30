The middle tier of the pyramid contains component-level integration tests. These could take the form of API tests in which a service is treated as a black box. For a variety of data inputs, the tests assert that the correct responses are returned. There are likely to be more of these kinds of tests than automated UI tests, but not so many that they become neglected and brittle.

The bottom tier of the pyramid is the largest and represents the unit tests.

There are no absolute numbers that can be applied to these layers. The pyramid simply maintains that one layer should be relatively smaller or larger than another. An order of magnitude might be a good guideline to follow, because it allows the actual number to remain relative. If there are hundreds of unit tests for a system, there should be only tens of component-level tests and only a handful of automated user interface tests. The numbers can scale up or down from there, with the smallest systems not requiring high-level tests at all.

# Testing pyramid anti-patterns

Sketching the testing pyramid for a system can be a useful diagnostic tool for problems with the code's adaptability. If mapping the relative quantity of tests at each level forms a shape other than a pyramid, there are too many or too few of a category of tests.

# The hourglass

Figure 5-10 shows what happens when a test pyramid is too top-heavy: it becomes an hourglass.

![](bbox=[0.18, 0.7, 0.48, 0.92])

FIGURE 5-10 When it has too many integration and acceptance tests, code is difficult to change.

When there are too many high-level tests, developers are burdened with the maintenance effort of ensuring that these tests run to completion. They also must write new tests, often at a rate at which the cost outweighs the benefit. Recall that testing gives you confidence that something is working.