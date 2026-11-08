
3. Remove duplication.
4. Decrease elements.

The numbers are both the order in which these are executed and the priority they are given.

Point 1 is self-evident. The code must pass all the tests. The code must work.

Point 2 says that after the code is made to work, it should then be made expressive. It should reveal the intention of the programmer. It should be easy to read and self-descriptive. This is where we apply many of the simpler and more cosmetic refactorings. We also split large functions into smaller, better-named functions.

Point 3 says that after we have made the code as descriptive and expressive as possible, we hunt for and remove any duplication within that code. We don’t want the code to say the same thing more than once. During this activity, the refactorings are usually more complicated. Sometimes removing duplication is as simple as moving the duplicate code into a function and calling it from many places. Other times it requires more interesting solutions, such as the Design Patterns:⁴ *Template Method, Strategy, Decorator,* or *Visitor*.

Point 4 says that once we have removed all the duplication, we should strive to decrease the number of structural elements, such as classes, functions, variables, etc.

The goal of Simple Design is to keep the *design weight* of the code as small as practicable.

⁴ Design Patterns are beyond the scope of this book. See Gamma, E., R. Helm, R. Johnson, and J. Vlissides. 1995. *Design Patterns: Elements of Reusable Object-Oriented Software*. Reading, MA: Addison-Wesley.

## What Is Pairing?

Pairing is the act of two people working together on a single programming problem. The pair may work together at the same workstation, sharing the screen, keyboard, and mouse. Or they may work on two connected workstations so long as they see and manipulate the same code. The latter option works nicely with popular screen-sharing software. That software also allows the partners to be remote from each other, so long as they have a good data and voice link.

Pairing programmers sometimes adopt different roles. One may be the driver and the other the navigator. The driver has the keyboard and mouse; the navigator takes a longer view and makes recommendations. Another role option is for one programmer to write a test, and the other to make it pass and write the next test for the first programmer to pass. This is sometimes called *Ping-Pong*.

Most often, however, there are no roles at all. The programmers are simply co-equal authors sharing the mouse and keyboard in a cooperative manner.

Pairs are not scheduled. They form and break up according to the programmers’ preference. Managers should not try to create pairing schedules or pairing matrices.

Pairs are generally short-lived. A pairing session can last as long as a day, but more often they last no more than an hour or two. Even pairings as short as 15 to 30 minutes can be beneficial.

Stories are not assigned to pairs. Individual programmers, and not pairs, are responsible for completing stories. The duration of a story is generally much longer than a single pairing.

Over the course of a week, each programmer will spend about half of their pairing time on their own tasks, recruiting the help of several others. The other half of their pairing time will be spent helping others with their tasks.

Seniors should take care to pair with juniors more often than they pair with other seniors. Juniors should request the help of seniors more often than they request the help of other juniors. Programmers with specialties should spend significant amounts of their pairing time working with programmers outside of their specialty. The goal is to spread and exchange knowledge, not concentrate it.

## Why Pair?

We pair so that we behave like a team. The members of a team do not work in isolation from each other. Instead, they collaborate on a second-by-second basis. When a member of a team goes down, the other team members cover the hole left by that member and keep making progress towards the goal.

Pairing is the best way, by far, to share knowledge between team members and prevent knowledge silos from forming. It is the best way to make sure that nobody on the team is indispensable.

Many teams have reported that pairing reduces errors and improves design quality. This is likely true in most cases. It is generally better to have more than one set of eyes on any given problem. Indeed, many teams have replaced code reviews with pairing.

## Pairing as Code Review

Pairing is a form of code review, but with a significant advantage. The pairing programmers are co-authors during the time they are pairing. They see older code and review it as a matter of course, but with the intention of authoring new code. Thus, the review is not simply a static check to ensure that the team’s coding standards are applied. Rather, it is a dynamic review of the current state of the code with an eye to where the code needs to be in the near future.

## What About the Cost?

It is hard to measure the cost of pairing. The most direct cost is that there are two people working on a single problem. It should be obvious that this does not double the effort to solve the problem; however, it does likely cost something. Various studies have indicated that the direct cost might be about 15%. In other words, it would require 115 pairing programmers to do the same work of 100 individuals (without code reviews).

A naive calculation would suggest that a team that pairs 50% of the time would suffer something less than 8% in productivity. On the other hand, if the practice of pairing replaces code reviews, then there is likely no reduction in productivity at all.

Then we must consider the benefits of the cross-training knowledge exchange and intense collaboration. These benefits are not easily quantifiable, but they are also likely significant.

My experience and the experience of many others is that pairing, when done informally and at the programmers’ discretion, is quite beneficial to the whole team.

## Just Two?

The word “pair” implies that there are just two programmers involved in a pairing session. While this is typically true, it is not a rule. Sometimes three, four, or more will decide to work together on a given problem. (Again, this is at the programmers’ discretion.) This is sometimes known as “mob programming.”⁵,⁶

⁵ https://en.wikipedia.org/wiki/Mob_programming

⁶ https://mobprogramming.org/mob-programming-basics/

## Management

Programmers often fear that managers will frown upon pairing and might even demand that pairs break up and stop wasting time. I’ve never seen this happen. In the half-century that I’ve been writing code, I’ve never seen a manager interfere at such a low level. Generally, in my experience, managers are pleased to see programmers collaborating and working together. It creates the impression that work is being done.

If, however, you are a manager who is tempted to interfere with pairing because you fear it is inefficient, then set your fears aside and let the programmers figure this out. They are, after all, the experts. And if you are a programmer whose manager has told you to stop pairing, remind that manager that you are the expert, and that therefore you, and not the manager, must be in charge of the way you work.

Finally, never, ever, ever, ask for permission to pair. Or test. Or refactor. Or… You are the expert. You decide.

## Conclusion

The technical practices of Agile are the most essential ingredient of any Agile effort. Any attempt to employ Agile practices without the technical practices is doomed to fail. The reason for this is simply that Agile is an efficient mechanism for making a big mess in a big hurry. Without the technical practices to keep the technical quality high, the productivity of the team will quickly falter and begin an inexorable death spiral.
