
### The Continuous Build

Once an acceptance test passes, it goes into the suite of tests that is run during the continuous build.

The continuous build is an automated procedure that runs every time³ a programmer checks code into the source code control system. This procedure builds the system from source and then runs the suites of automated programmer unit tests and automated acceptance tests. The results of that run are visibly posted, often in an email to every programmer and interested party. The state of the continuous build is something everyone should be continuously aware of.

³ Within a few minutes.

The continuous running of all these tests ensures that subsequent changes to the system do not break working features. If a previously passing acceptance test fails during the continuous build, the team must immediately respond and repair it before making any other changes. Allowing failures to accumulate in the continuous build is suicidal.

## II The Standards

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_273_0.png)

Standards are baseline *expectations*. They are the lines in the sand that we decide we cannot cross. They are the parameters we set as the minimum we can accept. Standards can be exceeded, but we must never fail to meet them.

## Your New CTO

Imagine that I am your new CTO. I’m going to tell you what I expect of you. You will read these expectations, and you will view them from two contradictory perspectives.

The first will be the perspective of your managers, executives, and users. And, from their perspective, these expectations will seem obvious and normal. No manager, executive, or user would ever expect less.

As a programmer, you may be more familiar with the second perspective. It is that of the programmers, architects, and technical leads. From their perspective, these expectations will seem extreme, impossible, even insane.

The difference in those two perspectives, the mismatch of those expectations, is the primary failing of the software industry, and it is one that we must urgently repair.

> > *As your new CTO, I expect. ...*

## 9 Productivity

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_275_0.png)

As your CTO, I have a couple of expectations about productivity.

### We Will Never Ship S**T

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_276_0.png)

As your new CTO, I expect that we will never ship S**T.

I’m sure you know what S**T stands for. As your CTO, I expect that *we will not ship S**T.*

Have you ever shipped S**T? Most of us have. I have. It didn’t feel good. I didn’t like it. The users didn’t like it. The managers didn’t like it. *Nobody* liked it.

So why do we do it? Why do we ship S**T?

Because somehow or another, we decided that we had no choice. Perhaps it was a deadline that we just absolutely had to meet. Maybe it was an estimate that we were too embarrassed to miss. Maybe it was just downright sloppiness or carelessness. Maybe it was management pressure. Maybe it was a matter of self-worth.

Whatever the reason, it was *invalid.* It is an absolute minimum standard that we will not ship S**T.

What is S**T? I’m sure you already know, but let’s go over it anyway.

- Every bug you ship is S**T.
- Every untested function is S**T.
- Every poorly written function is S**T.
- Every dependency on detail is S**T.
- Every unnecessary coupling is S**T.
- SQL in the GUI is S**T.
- Database schema in the business rules is S**T.

I could go on. But let me cut this short. Every failure of one of the disciplines in the foregoing chapters risks shipping S**T.

That doesn’t mean that every single one of those disciplines must be upheld at all times.

We are engineers. Engineers make trade-offs. But an engineering trade-off is not careless or sloppy. If you must break a discipline, you’d better have a good reason.

More important, you’d better have a good mitigation plan.

For example, let us say that you are writing Cascading Style Sheets (CSS) code. Writing automated tests up front for CSS is almost always impractical. You don’t really know how the CSS will render until you actually see it on the screen.

So how are we going to mitigate the fact that CSS breaks the test-driven development testing discipline?

We’re going to have to test the CSS manually, with our eyeballs. We’re also going to have to test it in all the browsers that our customers are likely to use. So, we’d better come up with a standard description of what we want to see on the screen and how much variation we can tolerate. Even more important, we’d better come up with a technical solution that makes that CSS easy to manually test because we, not QA, are going to test it before we ever release it from development.

Let me say this all another way: *Do a good job!*

That’s what everyone really expects. All our managers, all our users, everyone who ever touches or is touched by our software, expects us to have done a good job. We must not let them down.

I expect we will never ship S**T.

### Inexpensive Adaptability

*Software* is a compound word that means “flexible product.” The entire reason that software exists is so that we can quickly and easily change the behavior of our machines. To the extent that we build software that is hard to change, we thwart the very reason that software exists.

And yet inflexibility of software remains a huge problem in our industry. The reason we focus so much on design and architecture is to improve the flexibility and maintainability of our systems.

Why does software become rigid, inflexible, and fragile? Again, it is because software teams fail to engage in the testing and refactoring disciplines that support flexibility and maintainability. In some cases, those teams may depend solely on initial design and architecture efforts. In other cases, they may depend on fads that make unsustainable promises.

But no matter how many microservices you create, no matter how well structured your initial design and architectural vision is, without the testing and refactoring disciplines, the code will rapidly degrade and the system will become harder and harder to maintain.

I do not expect this. I expect that when customers ask for changes, the development team will be able to respond with a strategy that involves an expense that is *proportional to the scope of the change*.

Customers may not understand the internals of the system, but they have a good sense of the scope of the changes they request. They understand that a change may affect many features. They expect the cost of that change to be relative to the scope of that change.

Unfortunately, too many systems become so inflexible over time that the cost of change rises to a level that customers and managers cannot rationalize against the scope of the changes they request. To make matters worse, it is not uncommon for developers to rail against certain kinds of change on the basis that the change is against the architecture of the system.

An architecture that resists the changes that a customer requests is an architecture that thwarts the meaning and intent of software. Such an architecture must be changed to accommodate the changes that the customers will make. Nothing makes such changes easier than a well-refactored system and a suite of tests that you trust.

I expect that the design and architecture of the system will evolve with the requirements. I expect that when customers request changes, those changes will not be impeded by existing architecture or the rigidity and fragility of the existing system.

I expect inexpensive adaptability.

### We Will Always Be Ready

As your new CTO, I expect that we will always be ready.

Long before Agile made it popular, it was well understood by most software experts that well-run projects experience a regular rhythm of deployment and release. In the very early days, this rhythm tended to be quick: weekly or even daily. However, the waterfall movement that began in the 1970s greatly slowed the rhythm into months, sometimes years.

The advent of Agile, at the turn of the millennium, reasserted the need for faster rhythms. Scrum recommended sprints of 30 days. XP recommended iterations of 3 weeks. Both quickly increased the rate to biweekly. Nowadays, it is not uncommon for development teams to deploy multiple times per day, effectively reducing the development period to near zero.

I expect a quick rhythm. One or two weeks at most. And at the end of each sprint, I expect that the software will be technically ready to release.

*Technically ready to release* does not mean that the business will want to release it. The technically ready software may not have a feature set that the business deems complete or appropriate for its customers and users. Technically ready simply means that if the business decides to release it, the development team, including QA, has no objections. The software works, has been tested, has been documented, and is ready for deployment.

This is what it means to *always be ready*. I do not expect the development team to tell the business to wait. I do not expect long burn-in periods or so-called *stabilization sprints*. Alpha and beta testing may be appropriate to
