# ACCEPTANCE TESTS

The practice of Acceptance Tests is one of the least understood, least used, and most confused of all the Agile practices. This is strange because the underlying idea is remarkably simple: *Requirements should be specified by the business.*

The problem, of course, is the meaning of the word: *specify.* Many businesses would like that word to mean that they can wave their hands around in the air and describe the desired behavior in vague and fluffy terms. They want the developers to figure out all the little details. Many programmers would like the business to define *precisely* what the system should do, right down to the coordinates and values of each individual pixel.

Something in the middle of these two extremes is necessary.

So what is a specification? A specification is, by its very nature, *a test.* For example:

> > *When the user enters a valid username and password, and then clicks “login,” the system will present the “Welcome” page.*

This is obviously a specification. It is also obviously a test.

It should also be obvious that this test could be automated. There is no reason that a computer could not verify that the specification has been met.

This is the practice of Acceptance Tests. The practice says that, to the degree practicable, the requirements of the system should be written as automated tests.

But wait! Who writes these automated tests? The first paragraph in this section answers that question: *Requirements should be specified by the business.* So the business should write the automated tests. Right?