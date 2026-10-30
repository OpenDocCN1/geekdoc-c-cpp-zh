The Scrum board can be further split by using horizontal swimlanes. These swimlanes can be used to group the stories by feature, so that everyone can see at a glance where effort is being concentrated, and thus where bottlenecks need to be alleviated.

One special swimlane at the top of the board is the Fast-Track lane, into which any very high–priority tasks can be placed. Team members can be instructed to "swarm" on a fast-track item so that it is completed as quickly as possible, often to the detriment of any other outstanding work. Swarming ensures that the team stops what they are doing to collaborate on a problem or task that has overriding priority. It is a useful tool and should be used sparingly, when such a priority occurs. Apocalyptic defects found in production are the most common fast-track items.

# Technical debt

The term technical debt deserves further explanation. Throughout the course of implementing a user story, it is likely that certain compromises will need to be made between the "ideal code" and code that is good enough to meet the deadline. This is not to say that poor design should be tolerated or encouraged in order to hit a deadline, but that there is value in doing something simpler now, with a view to improving it later.

# Good and bad technical debt

Debt is likely to accrue gradually over the lifetime of a project. It is termed debt because that is a great metaphor for how it should be viewed. There is nothing wrong with certain types of financial debt. If, for example, you have the option of spreading the payments for a car over 12 months with low-interest repayments, you are in debt. But this could be a good decision if you need the car for commuting and cannot afford the payment in full. The car will allow you to generate the revenue necessary to pay the repayments, because you can now get to work on time.

Of course, some debt is bad. If you take out a credit card and pay for something extravagant without first calculating how you will repay the debt, you can end up in a cycle of balance transfers, trying to keep interest payments at a minimum. This will, in hindsight, look like a bad financial decision based around bad debt. The key is to look carefully at the options and decide whether the debt is worth taking on or whether you should just pay up front.

The tradeoff is the same in software. You could implement a suboptimal solution now and meet a deadline or spend the extra time now to improve the design, perhaps missing the deadline. There is no right answer that fits all situations, just guidelines for detecting good and bad technical debt.

# The technical debt quadrant

Martin Fowler, a prominent Agile evangelist, defined a technical debt quadrant for categorizing the concessions and compromises that might be needed to mark a story as done. The two axes that divide a plane into quadrants, x and y, correspond to the questions, "Are we accruing this technical debt for the correct reasons?" and "Are we aware of alternatives to avoid this technical debt?", respectively.

If you answer "Yes" to the former question, you are adding prudent technical debt: you can point to valid reasons for adding it, and your conscience is clear. If you answer "No," this debt is reckless and you would be better advised to deal with this debt now, rather than allow it to accumulate.