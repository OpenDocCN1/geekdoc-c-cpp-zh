
## Do Prerequisites Apply to Modern Software Projects?

> The methodology used should be based on choice of the latest and best, and not based on ignorance. It should also be laced liberally with the old and dependable.
> —Harlan Mills

Some people have asserted that upstream activities such as architecture, design, and project planning aren’t useful on modern software projects. In the main, such assertions are not well supported by research, past or present, or by current data. (See the rest of this chapter for details.) Opponents of prerequisites typically show examples of prerequisites that have been done poorly and then point out that such work isn’t effective. Upstream activities can be done well, however, and industry data from the 1970s to the present day indicates that projects will run best if appropriate preparation activities are done before construction begins in earnest.

![](img/649c8eee28c38ca1e062691e45dc9883_61_0.png)

The overarching goal of preparation is risk reduction: a good project planner clears major risks out of the way as early as possible so that the bulk of the project can proceed as smoothly as possible. By far the most common project risks in software development are poor requirements and poor project planning, thus preparation tends to focus on improving requirements and project plans.

Preparation for construction is not an exact science, and the specific approach to risk reduction must be decided project by project. Details can vary greatly among projects. For more on this, see Section 3.2.

## Causes of Incomplete Preparation

You might think that all professional programmers know about the importance of preparation and check that the prerequisites have been satisfied before jumping into construction. Unfortunately, that isn’t so.

Further Reading For a description of a professional development program that cultivates these skills, see Chapter 16 of Professional Software Development (McConnell 2004).

A common cause of incomplete preparation is that the developers who are assigned to work on the upstream activities do not have the expertise to carry out their assignments. The skills needed to plan a project, create a compelling business case, develop comprehensive and accurate requirements, and create high-quality architectures are far from trivial, but most developers have not received training in how to perform these activities. When developers don’t know how to do upstream work, the recommendation to “do more upstream work” sounds like nonsense: If the work isn’t being done well in the first place, doing more of it will not be useful! Explaining how to perform these activities is beyond the scope of this book, but the “Additional Resources” sections at the end of this chapter provide numerous options for gaining that expertise.

Some programmers do know how to perform upstream activities, but they don’t prepare because they can’t resist the urge to begin coding as soon as possible. If you feed your horse at this trough, I have two suggestions. Suggestion 1: Read the argument in the next section. It may tell you a few things you haven’t thought of. Suggestion 2: Pay attention to the problems you experience. It takes only a few large programs to learn that you can avoid a lot of stress by planning ahead. Let your own experience be your guide.

A final reason that programmers don’t prepare is that managers are notoriously unsympathetic to programmers who spend time on construction prerequisites. People like Barry Boehm, Grady Booch, and Karl Wiegers have been banging the requirements and design drums for 25 years, and you’d expect that managers would have started to understand that software development is more than coding.

Further Reading For many entertaining variations on this theme, read Gerald Weinberg’s classic, The Psychology of Computer Programming (Weinberg 1998).

A few years ago, however, I was working on a Department of Defense project that was focusing on requirements development when the Army general in charge of the project came for a visit. We told him that we were developing requirements and that we were mainly talking to our customer, capturing requirements, and outlining the design. He insisted on seeing code anyway. We told him there was no code, but he walked around a work bay of 100 people, determined to catch someone programming. Frustrated by seeing so many people away from their desks or working on requirements and design, the large, round man with the loud voice finally pointed to the engineer sitting next to me and bellowed, “What’s he doing? He must be writing code!” In fact, the engineer was working on a document-formatting utility, but the general wanted to find code, thought it looked like code, and wanted the engineer to be working on code, so we told him it was code.

This phenomenon is known as the WISCA or WIMP syndrome: Why Isn’t Sam Coding Anything? or Why Isn’t Mary Programming?

If the manager of your project pretends to be a brigadier general and orders you to start coding right away, it’s easy to say, “Yes, Sir!” (What’s the harm? The old guy must know what he’s talking about.) This is a bad response, and you have several better alternatives. First, you can flatly refuse to do work in an ineffective order. If your relationships with your boss and your bank account are healthy enough for you to be able to do this, good luck.

A second questionable alternative is pretending to be coding when you’re not. Put an old program listing on the corner of your desk. Then go right ahead and develop your requirements and architecture, with or without your boss’s approval. You’ll do the project faster and with higher-quality results. Some people find this approach ethically objectionable, but from your boss’s perspective, ignorance will be bliss.

Third, you can educate your boss in the nuances of technical projects. This is a good approach because it increases the number of enlightened bosses in the world. The next subsection presents an extended rationale for taking the time to do prerequisites before construction.

Finally, you can find another job. Despite economic ups and downs, good programmers are perennially in short supply (BLS 2002), and life is too short to work in an unenlightened programming shop when plenty of better alternatives are available.

## Utterly Compelling and Foolproof Argument for Doing Prerequisites Before Construction

Suppose you’ve already been to the mountain of problem definition, walked a mile with the man of requirements, shed your soiled garments at the fountain of architecture, and bathed in the pure waters of preparedness. Then you know that before you implement a system, you need to understand what the system is supposed to do and how it’s supposed to do it.

![](img/649c8eee28c38ca1e062691e45dc9883_63_0.png)

Part of your job as a technical employee is to educate the nontechnical people around you about the development process. This section will help you deal with managers and bosses who have not yet seen the light. It’s an extended argument for doing requirements and architecture—getting the critical aspects right—before you begin coding, testing, and debugging. Learn the argument, and then sit down with your boss and have a heart-to-heart talk about the programming process.

### Appeal to Logic

One of the key ideas in effective programming is that preparation is important. It makes sense that before you start working on a big project, you should plan the project. Big projects require more planning; small projects require less. From a management point of view, planning means determining the amount of time, number of people, and number of computers the project will need. From a technical point of view, planning means understanding what you want to build so that you don’t waste money building the wrong thing. Sometimes users aren’t entirely sure what they want at first, so it might take more effort than seems ideal to find out what they really want. But that’s cheaper than building the wrong thing, throwing it away, and starting over.

It’s also important to think about how to build the system before you begin to build it. You don’t want to spend a lot of time and money going down blind alleys when there’s no need to, especially when that increases costs.

### Appeal to Analogy

Building a software system is like any other project that takes people and money. If you’re building a house, you make architectural drawings and blueprints before you begin pounding nails. You’ll have the blueprints reviewed and approved before you pour any concrete. Having a technical plan counts just as much in software.
