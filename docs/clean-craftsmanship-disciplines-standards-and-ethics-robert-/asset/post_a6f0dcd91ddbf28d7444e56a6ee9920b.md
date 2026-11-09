
Automated tests *should not test business rules through the user interface.* User interfaces are subject to change for reasons that have more to do with fashion, facility, and general marketing chaos than with business rules. When automated tests are driven through the user interface, as shown in [Figure 10.1](#figure-10-1), those tests are subject to those changes. As a consequence, the tests become very fragile, which often results in the tests being discarded as too difficult to maintain.

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_289_0.png)

**Figure 10.1** Tests driven through the user interface

To avoid this situation, developers should isolate the business rules from the user interface with a function call API, as shown in [Figure 10.2](#figure-10-2). Tests that use this API are completely independent of the user interface and are not subject to interface changes.

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_290_0.png)

**Figure 10.2** Tests through the API are independent of the user interface.

### Testing the User Interface

If the business rules are automatically tested through a function call API, then the amount of testing required for the behavior of the user interface is vastly reduced. Care should be taken to maintain the isolation from the business rules by replacing the business rules with a stub that supplies canned values to the user interface, as shown in Figure 10.3.

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_291_0.png)

**Figure 10.3** The stub supplies canned values to the user interface.

Doing so ensures that the tests of the user interface will be fast and unambiguous. If the user interface is significantly large and complex, then an automated user interface testing framework may be appropriate. The use of the business rule stub will make those tests much more reliable.

If the user interface is small and simple, it may be more expeditious to fall back on manual testing, especially if there are aesthetics to be evaluated. Again, the use of the business rule stub will make these manual tests much easier to conduct.

I expect that every test that can practically be automated *will* be automated, that the tests will execute quickly, and that the tests will not be fragile.

## 11 Courage

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_292_0.png)

As CTO, I have several expectations related to courage.

### We Cover for Each Other

We use the word *team* to describe a group of developers working on a project. But do we understand what a team really is?

A team is a group of collaborators who understand their goals and their interaction so well that when a team member goes down for some reason, *they keep* making progress toward their goal. For example, every crew member on board a ship has a job to do. Every crew member also knows how to do someone else’s job—for obvious reasons. The ship has to keep sailing even when a crew member goes down.

I expect that the members of a programming team will cover for each other like the crew of a ship. When a team member goes down, I expect others on the team to take over that role until the fallen team member resumes their place on the team.

People on a team can go down for many reasons. They may get sick. They may be distracted by trouble at home. They may go on vacation. Work on the project cannot stop. Others must fill the hole left behind.

If Bob is the database guy, and Bob goes down, someone else must pick up the database work and keep making progress. If Jim is the GUI guy, and Jim goes down, someone else must pick up the GUI work and continue to make progress.

This means that each member of the team must be familiar with more than just their own work. They must be familiar with the work of others so that they can step in if one of those others goes down.

But let me turn this around. It is *your* responsibility to make sure someone can cover for *you*. It is your responsibility to ensure that *you* are not the *one* indispensable player on the team. It is your responsibility to seek out others and teach them enough about your work that they can take over for you in a pinch.

How can you teach others about your work? Probably the best way is to sit down with them at a workstation and write code together for an hour or so. And if you are wise, you will do this with more than one other member of the team. The more people who know your work, the more people can cover for you if you go down.

And remember, once is not enough. As you continue to make progress on your part of the project, you’ll have to continually keep the others abreast of your work. You will find the discipline of collaborative programming helpful in this regard.

I expect that the members of programming teams will be able to cover for each other.

### Honest Estimates

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_294_0.png)

I expect honest estimates.

As a programmer, the most honest estimate you can give is “I don’t know” because you actually do not know how long the task will take. On the other hand, you do know that you will probably finish the task in less than a billion years. So, an honest estimate is an amalgam of what you don’t know with what you do know.

An honest estimate looks something like this:

- I have a 5 percent chance of finishing this task before Friday.
- I have a 50 percent chance of finishing before the next Friday.
- I have a 95 percent chance of finishing before the Friday after that.

An estimate like this provides a probability distribution that describes your uncertainty. Describing your uncertainty is what makes this estimate honest.

You should provide estimates in this form when managers ask you to estimate large projects. For example, they may be trying to judge the cost of a project before they authorize it. That's when this kind of honesty about uncertainty is most valuable.

For smaller tasks, it is best to use the Agile practice of story points. Story points are honest because they do not commit to a timeframe. Rather, they describe the cost of a task in comparison to another. The numbers used are arbitrary, but relative.

A story point estimate looks something like this:

> *The Deposit story has a cost of 5.*

What is that 5? It's an arbitrary number of points that is relative to some task of known size. For example, let's say that the Login story was arbitrarily given 3 points. When you estimate the Deposit story, you decide that Deposit is not quite twice as hard as Login, so you give it a 5. That's really all there is to it.

Story points already have the probability distribution embedded within them. First, the points are not dates or times; they are just points. Second, the points are not promises; they are guesses. At the end of each Agile iteration (usually a week or two), we total the points completed. We use that number to estimate how many points we might complete in the next iteration.

I expect honest estimates that describe your uncertainty. I do not expect a promise of a date.

### You Must Say NO

I expect you to say no when the answer is no.

One of the most important things a programmer can say is “No!” Said at the right time, in the right context, this answer can save your employer massive amounts of money and prevent horrible failures and embarrassments.

This is not a license to storm around saying no to everything. We are engineers; our job is to find a way to yes. But sometimes yes is not an option. We are the only ones who can determine this. We are the ones who know. Therefore, it is up to us to say no when the answer really is no.

Let’s say your boss asks you to get something done by Friday. After giving it due consideration, you realize that there is no reasonable chance that you’ll complete the task by Friday. You must return to your boss and say “No.” You would be wise to also say that you can get it done by the following Tuesday, but you must be firm that Friday is out of the question.

Managers often don’t like to hear no. They may push back on you. They may confront you. They may yell at you. Emotional confrontation is one of the tools that some managers employ.

You must not give in to it. If the answer is no, then you must hold to that answer and not yield to the pressure.

And be very wary of the “Will you at least try?” gambit. It seems so reasonable to be asked to try, doesn’t it? But it’s not reasonable at all because *you are already trying*. There’s nothing new you can do to change the no to yes, so saying you’ll try is just a lie.

I expect that when the answer is no, you will say no.

### Continuous Aggressive Learning
