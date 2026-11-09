Long story short—I got a special-purpose, one-of-a-kind unit up and running for the customer in two weeks. We called it the pCCU.

# # The Lesson

Those two stories are examples of the huge range that estimates can have. On the one hand, I underestimated the vectoring of the chips by a factor of six. On the other, we found a solution to the CCU/CMU in one-twentieth the expected time.

This is where honesty comes in. Because, honestly, when things go wrong, they can go very, very wrong. And when things go right, they can sometimes go very, very right.

This makes estimating, one hell of a challenge.

# # Accuracy

It should be clear by now that an estimate for a project *cannot* be a date. A single date is far too precise for a process that can be off by as much as a factor of 6, or even 20.

Estimates are not dates. Estimates are ranges. Estimates are *probability distributions*.

Probability distributions have a mean and a width—sometimes called the *standard deviation* or the *sigma*. We need to be able to express our estimates as both the mean and the sigma.

Let’s first look at the mean.

Finding the expected mean completion time for a complex task is a matter of adding up all the mean completion times for all of the subtasks. And, of course, this is recursive. The subtasks can be estimated by adding up all the times for the sub-subtasks. This creates a tree of tasks that is often called a work breakdown structure (WBS).