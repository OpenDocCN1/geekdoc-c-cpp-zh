
Now, this is all well and good. The problem, however, is that we are not very good at identifying all the subtasks and sub-subtasks, and sub-sub-subtasks. Generally, we miss a few. Like, maybe, half.

We compensate for this by multiplying the sum by two. Or sometimes three. Or maybe even more.

**Kirk:** *How much refit time until we can take her out again?*

**Scotty:** Eight weeks, sir. But you don’t have eight weeks, so I’ll do it for you in two.

**Kirk:** Mr. Scott, have you always multiplied your repair estimates by a factor of four?

**Scotty:** Certainly, sir! How else can I keep my reputation as a miracle worker?³

3. *Star Trek II: The Wrath of Khan*, directed by Nicholas Meyer (Paramount Pictures, 1982).

Now this fudge factor of 2, or 3, or even 4, sounds like cheating. And, of course, it is. But so is the very act of estimating.

There is only one real way to determine how long something is going to take, and that’s by doing it. Any other mechanism is cheating.

So, face it, we’re going to cheat. We’re going to do the WBS and then multiply by some *F*, where *F* is between 2 and 4, depending on your confidence and productivity. That will give us our mean time to completion.

Managers are going to ask you how you came up with your estimates, and you’re going to have to tell them. And when you tell them about that fudge factor, they’re going to ask you to reduce it by spending more time on the WBS.

This is perfectly fair, and you should be willing to comply. However, you should also warn them that the cost of developing a complete WBS is equivalent to the cost of the task itself. Indeed, by the time you *have* developed the complete WBS, you will also have completed the project, because the only way to truly enumerate all the tasks is by executing the tasks you know about in order to discover the rest—recursively.

So, make sure you put your estimation effort into a timebox, and let your managers know that getting better refinement on the fudge factor is going to be very expensive.

There are many techniques for estimating the subtasks at the leaves of the WBS tree. You could use function points or a similar complexity measure. But I’ve always found that these tasks are best estimated by raw gut feel.

Typically, I do this by comparing the tasks to some other tasks that I’ve already completed. If I think it’s twice as hard, I multiply the time by two.

Once you’ve estimated all the leaves of the tree, you just sum the whole tree up to get the mean for the project.

And don’t worry overmuch about dependencies. Software is a funny material. Even though A depends on B, B often does not have to be done before A. You *can*, in fact, implement logout before you implement login.

## Precision

Every estimate is wrong. That’s why we call it an estimate. An estimate that is correct is not an estimate at all—it’s a fact.

But even though the estimate is wrong, it may not be all that wrong. Part of the job of estimation, then, is to estimate how wrong the estimate is.

My favorite technique for estimating how wrong an estimate is, is to estimate three numbers: the best case, the worst case, and the normal case.

The normal case is how long you think the task would take you if the average number of things go wrong—if things go the way they *usually* do. Think of it like a gut-level call. The normal case is the estimate you would give if you were being realistic.

The strict definition of a normal estimate is one that has a 50 percent chance of being too short or too long. In other words, you should miss half of your normal estimates.

The worst-case estimate is the Murphy’s law estimate. It assumes that anything that can go wrong will go wrong. It is deeply pessimistic. The worst-case estimate has a 95 percent chance of being too long. In other words, you would only miss this estimate 1 in 20 times.

The first thing we want to do is represent each task in terms of its expected completion time and the standard deviation.

Now remember, 6 standard deviations (3 on each side of the mean) corresponds to a probability of better than 99 percent. So, we’re going to set our standard deviation, our sigma, to Worst minus Best over 6.

The expected completion time (mu) is a bit trickier. Notice that N is probably not equal to (W-B), the midpoint. Indeed, the midpoint is probably well past N because it is much more likely for a project to take more time than we think than less time. So, on average, when will this task be done? What is the *expected* completion time?

It’s probably best to use a weighted average like this: mu = (2N + (B + W)/2)/3.

Now we have calculated the mu and sigma for a set of tasks. The expected completion time for the whole project is just the sum of all the mus. The sigma for the project is the square root of the sum of the squares of all the sigmas.

This is just basic statistical mathematics.

What I’ve just described is the estimation procedure invented back in the late 1950s to manage the Polaris Fleet Ballistic Missile program. It has been used successfully on many thousands of projects since.

It is called PERT—the program evaluation and review technique.

## Honesty

We started with honesty. Then we talked about accuracy, and we talked about precision. Now it’s time to come back to honesty.

The kind of estimating we are talking about here is intrinsically honest. It is a way of communicating, to those who need to know, the level of your uncertainty.

This is honest because you truly are uncertain. And those with the responsibility to manage the project must be aware of the risks that they are taking so that they can manage those risks.

One of the prime values you bring to the organization is your ability to know when the answer must be no. By saying no at those times, you will save your company untold grief and money.

One last thing. Often, managers will try to cajole you into committing—into saying yes. Watch out for this.

They might tell you that you aren't being a team player or that other people have more commitment than you do. Don't be fooled by those games.

Be willing to work with them to find solutions, but don't let them bully you into saying yes when you know you shouldn't.

And be very careful with the word try. Your boss might say something reasonable, like “Well, will you at least try?”

The answer to this question is

> NO! I am already trying. How dare you suggest that I am not? I am trying as hard as I can, and there is no way I can try harder. There are no magic beans in my pocket with which I can work miracles.

You might not want to use those exact words, but that's exactly what you should be thinking.

And remember this. If you say, “Yes, I’ll try,” then you are lying. Because you have no idea how you are going to succeed. You don't have any plan to change your behavior. You said yes just to get rid of the manager. And that is fundamentally dishonest.

## Respect

> Promise 9. I will respect my fellow programmers for their ethics, standards, disciplines, and skill. No other attribute or characteristic will be a factor in my regard for my fellow programmers.

We, software professionals, accept the weighty burden of our craft. We brave folks are men and women, straight and gay, black, brown, yellow, and white, Republicans, Democrats, religious believers, and atheists. We are humans, in all the many forms and varieties that humans come in. We are a community of mutual respect.

The only qualifications for entry into our community and for receiving the acceptance and the respect of each and every member of that community are the skills, disciplines, standards, and ethics of our profession. No other human attribute is worthy of consideration. No discrimination on any other basis can be tolerated.

’Nuff said.

## Never Stop Learning

> *Promise 10. I will never stop learning and improving my craft.*

A programmer never stops learning.

I’m sure you’ve heard it said that you should learn a new language every year. Well, you should. A good programmer should know a dozen or so languages.

And not just a dozen varieties of the same language. Not just C, C++, Java, and C#. Rather, you should know languages from many different families.

You should know a statically typed language like Java or C#. You should know a procedural language like C or Pascal. You should know a logic language like Prolog. You should know a stack language like Forth. You should know a dynamically typed language like Ruby. You should know a functional language like Clojure or Haskell.

You should also know several different frameworks, several different design methodologies, and several different development processes. I don’t mean to say you should be an expert in all these things, but you should make a point to expose yourself to them at significantly more than a cursory level.

The list of things you should similarly expose yourself to is virtually endless. Our industry has experienced rapid change over the decades, and that change is likely to continue for some time. You have to keep up with it.

And that means you have to keep on learning. Keep reading books and blogs. Keep watching videos. Keep going to conferences and user groups. Keep going to training courses. Keep learning.
