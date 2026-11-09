
A stupid idea that works is not a stupid idea.

However, you can't leave that quick and dirty patch in place without causing harm. The longer that patch remains in the code, the more harm it can do.

Remember that the Knight Capital debacle would not have happened if the old Power Peg code had been removed from the code base. It was that old defunct code that actually made the bad trades.

What do we mean by "harm to structure"? Clearly, having thousands of global variables is a structural flaw. So is dead code left in the code base.

Structural harm is harm to the organization and content of the source code. It is anything that makes that source code hard to read, hard to understand, hard to change, or hard to reuse.

It is the responsibility of every professional software developer to know the disciplines and standards of good software structure. They should know how to refactor, how to write tests, how to recognize bad code, how to decouple designs and create appropriate architectural boundaries. They should know and apply the principles of low- and high-level design. And it is the responsibility of every senior developer to make sure that younger developers learn these things and satisfy them in the code that they write.

## Soft

The first word in software is *soft*. Software is supposed to be SOFT. It's supposed to be easy to change. If we didn't want it to be easy to change, we'd have called it *hardware*.

It's important to remember why software exists at all. We invented it as a means to make the behavior of machines easy to change. To the extent that our software is hard to change, we have thwarted the very reason that software exists.

Remember that software has two values. There's the value of its behavior, and then there's the value of its "softness." Our customers and users expect us to be able to change that behavior easily and without high cost.

Which of these two values is the greater? Which value should we prioritize above the other? We can answer that question with a simple thought experiment.

Imagine two programs. One works perfectly but is impossible to change. The other does nothing correctly but is easy to change. Which is the more valuable?

I hate to be the one to tell you this but, in case you hadn’t noticed, software requirements tend to change, and when they change, that first software will become useless—forever.

On the other hand, that second software can be made to work, because it’s easy to change. It may take some time and money to get it to work initially, but after that, it’ll continue to work forever with minimal effort.

Therefore, it is the second of the two values that should be given priority in all but the most urgent of situations.

What do I mean by *urgent*? I mean a production disaster that’s losing the company $10 million per minute. That’s urgent.

I do not mean a software startup. A startup is not an urgent situation requiring you to create inflexible software. Indeed, the opposite is true. The one thing that is absolutely certain in a startup is that you are creating the wrong product.

No product survives contact with the user. As soon as you start to put the product into users’ hands, you will discover that the product you’ve built is wrong in a hundred different ways. And if you can’t change it without making a mess, you’re doomed.

This is one of the biggest problems with software startups. Startup entrepreneurs believe they are in an urgent situation requiring them to throw out all the rules and dash to the finish line, leaving a huge mess in their wake. Most of the time, that huge mess starts to slow them down long before they do their first deployment. They’ll go faster and better and will survive a lot longer if they keep the structure of the software from harm.

> *When it comes to software, it never pays to rush.*
>
> —Brian Marick

## Tests

Tests come first. You write them first, and you clean them first. You will know that every line of code works because you will have written tests that prove they work.

How can you prevent harm to the behavior of your code if you don’t have the tests that prove that it works?

How can you prevent harm to the structure of your code if you don’t have the tests that allow you to clean it?

And how can you guarantee that your test suite is complete if you don’t follow the three laws of test-driven development (TDD)?

Is TDD really a prerequisite to professionalism? Am I really suggesting that you can’t be a professional software developer unless you practice TDD?

Yes, I think that’s true. Or rather, it is becoming true. It is true for some of us, and with time, it is becoming true for more and more of us. I think the time will come, and relatively soon, when the majority of programmers will agree that practicing TDD is part of the minimum set of disciplines and behaviors that mark a professional developer.

Why do I believe that?

Because, as I said earlier, we rule the world! We write the rules that make the whole world work.

In our society, nothing gets bought or sold without software. Nearly all correspondence is through software. Nearly all documents are written with software. Laws don’t get passed or enforced without it. There is virtually no activity of daily life that does not involve software.

Without software, our society does not function. Software has become the most important component in the infrastructure of our civilization.

Society does not understand this yet. We programmers don’t really understand it yet either. But the realization is dawning that the software we write is critical. The realization is dawning that many lives and fortunes depend on our software. And the realization is dawning that software is being written by people who do not profess a minimum level of discipline.

So, yes, I think TDD, or some discipline very much like it, will eventually be considered a minimum standard behavior for professional software developers. I think our customers and our users will insist on it.

## Best Work

> *Promise 2. The code that I produce will always be my best work. I will not knowingly allow code that is defective in either behavior or structure to accumulate.*

Kent Beck once said, “First make it work. Then make it right.”

Getting the program to work is just the first—and easiest—step. The second—and harder—step is to clean the code.

Unfortunately, too many programmers think they are done once they get a program to work. Once it works, they move on to the next program, and then the next, and the next.

In their wake, they leave behind a history of tangled, unreadable code that slows down the whole development team. They do this because they think their value is in speed. They know they are paid a lot, and so they feel that they must deliver a lot of functionality in a short amount of time.

But software is hard and takes a lot of time, and so they feel like they are going too slowly. They feel like they are failing, which creates a pressure that causes them to try to go faster. It causes them to rush. They rush to get the program working, and then they declare themselves to be done—because, in their minds, it’s already taken them too long. The constant tapping of the project manager’s foot doesn’t help, but that’s not the real driver.

I teach lots of classes. In many of them, I give the programmers small projects to code. My goal is to give them a coding experience in which to try out new techniques and new disciplines. I don’t care if they actually finish the project. Indeed, all the code is going to be thrown away.

Yet still I see people rushing. Some stay past the end of the class just hammering away at getting something utterly meaningless to work.

So, although the boss’s pressure doesn’t help, the real pressure comes from inside us. We consider speed of development to be a matter of our own self-worth.

## Making It Right

As we saw earlier in this chapter, there are two values to software. There is the value of its behavior and the value of its structure. I also made the point that the value of structure is more important than the value of behavior. This is because to have any long-term value, software systems must be able to react to changes in requirements.

Software that is hard to change is also hard to keep up to date with the requirements. Software with a bad structure can quickly get out of date.

In order for you to keep up with requirements, the structure of the software has to be clean enough to allow, and even encourage, change. Software that is easy to change can be kept up to date with changing requirements, allowing it to remain valuable with the least amount of effort. But if you’ve got a software system that’s hard to change, then you’re going to have a devil of a time keeping that system working when the requirements change.

When are requirements most likely to change? Requirements are most volatile at the start of a project, just after the users have seen the first few features work. That’s because they’re getting their first look at what the system actually does as opposed to what they thought it was going to do.

Consequently, the structure of the system needs to be clean at the very start if early development is to proceed quickly. If you make a mess at the start, then even the very first release will be slowed down by that mess.

Good structure enables good behavior and bad structure impedes good behavior. The better the structure, the better the behavior. The worse the structure, the worse the behavior. The value of the behavior depends critically on the structure. Therefore, the value of the structure is the most critical of the two values, which means that professional developers put a higher priority on the structure of the code than on the behavior.

Yes, first you make it work; but then you make very sure that you continue to make it right. You keep the system structure as clean as possible.
