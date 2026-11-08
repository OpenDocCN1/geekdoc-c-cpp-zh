
The year was 1995. My first book was scheduled to go to press the next day, and I was on the hook to deliver page proofs. It was 6 p.m. and I had them all ready to go. All I needed to do was to FTP them to my publisher.

But then, by sheer accident, I stumbled across a way to *double* the resolution of the hundreds of diagrams in that book. Jim and Jennifer were helping me get the page proofs ready, and we were just about to execute the FTP when I showed an example of the improved resolution to them.

We all looked at each other, heaved a great sigh, and Jim said, “We have to redo them all.” It wasn’t a question. It was a statement of fact. The three of us looked at each other, at the clock, back at each other, and then we buckled down and got to work.

But when we were done with that all-nighter, we were *done*. The book shipped. And we slept.

## SLEEP

The most precious ingredient in the life of a programmer is sufficient sleep. I do well on seven hours. I can tolerate a day or two of six hours. Anything less, and my productivity plummets. Make sure you know how many hours of sleep your body needs, and then prioritize those hours. Those hours will more than pay themselves back. My rule of thumb is that the first hour of insufficient sleep costs me two hours of daytime work. The second hour of insufficient sleep costs me another four hours of productive work. And, of course, there’s no productive work at all if I’m three hours behind on my sleep.

## COLLECTIVE OWNERSHIP

No one owns the code in an Agile project. The code is owned by the team as a whole. Any member of the team can check out and improve any module in the project at any time. The team owns the code *collectively*.

I learned *Collective Ownership* early in my career while working at Teradyne. We worked on a large system composed of fifty thousand lines of code partitioned into several hundred modules. Yet no one on the team owned any of those modules. We all strove to learn and improve all of those modules. Oh, some of us were more familiar with certain parts of the code than others, but we sought to spread rather than concentrate that experience.

That system was an early distributed network. There was a central computer that communicated with several dozen satellite computers that were distributed across the country. These computers communicated over 300-baud modem lines. There was no division between the programmers who worked on the central computer and the satellite computers. We all worked on the software for both of them.

These two computers had very different architectures. One was similar to a PDP-8 except that it had an 18-bit word. It had 256K of RAM and was loaded from magnetic tape cartridges. The other was an 8085 8-bit microprocessor with 32K of RAM and 32K of ROM.

We programmed these in assembler. The two machines had very different assembly languages and very different development environments. We all worked with both with equal comfort.

*Collective Ownership* does not mean that you cannot specialize. As systems grow in complexity, specialization becomes an absolute necessity. There are systems that simply cannot be understood in both entirety and detail. However, even as you specialize, you must also generalize. Divide your work between your specialty and other areas of the code. Maintain your ability to work outside of your specialty.

When a team practices *Collective Ownership*, knowledge becomes distributed across the team. Each team member gains a better understanding of the boundaries between modules and of the overall way that the system works. This drastically improves the ability of the team to communicate and make decisions.

In my rather long career, I have seen a few companies that practiced the opposite of *Collective Ownership*. Each programmer owned their own modules, and no one else was allowed to touch them. These were grossly dysfunctional teams who were constantly involved in finger pointing and miscommunication. All progress in a module would stop when the author was not at work. No one else dared to work on something owned by someone else.

## The X Files

One particularly maladroit case was the company X, which built high-end printers. In the 1990s, the company was transitioning from a predominant hardware focus to an integrated hardware and software focus. They realized that they could cut their manufacturing costs significantly if they used software to control the internal operation of their machines.

However, the hardware focus was deeply ingrained, so the software groups were divided along the same lines as the hardware. The hardware teams were organized by device: there were respective hardware teams for the feeder, printer, stacker, stapler, etc. The software was organized according to the same devices. One team wrote the control software for the feeder, another team wrote the software for the stapler, and so forth.

In X, your political clout depended on the device you worked on. Since X was a printer company, the printer device was the most prestigious. The hardware engineers who worked on the printer had to come up through the ranks to get there. The stapler guys were nobodies.

Oddly, this same political ranking system applied to the software teams. The developers writing the stacker code were politically important; but if a printer developer spoke in a meeting, everyone else listened closely. Because of this political division, no one shared their code. The key to the printer team’s political clout was locked up in the printer code. So the printer code stayed locked up, too. Nobody outside that team could see it.

The problems this caused were legion. There are the obvious communication difficulties when you can’t inspect the code you are using. There is also the inevitable finger pointing and backstabbing.

When he finally tried to check in and integrate his changes, he found that so many other changes had accumulated that the merge took him a long time to get working. While he was struggling with that merge, the other programmers continued to make 15-minute checkins. When he finally got his merge working and tried to check in his code, he found he had another merge to do.

He was so frustrated by this that he stood up in the middle of class and loudly proclaimed, “XP doesn’t work.” Then he stormed out of the classroom and went to the hotel bar.

And then a miracle happened. The pair partner that he had rejected went after him to talk him down. The other two pairs reprioritized their work, finished the merge, and got the project back on track. Thirty minutes later the student, now much calmer, came back in the room, apologized, and resumed his work—including pairing. He subsequently became an enthusiastic advocate for Agile development.

The point is that Continuous Integration only works if you integrate continuously.

## Then Came Continuous Build

In 2001, ThoughtWorks changed the game significantly. They created *CruiseControl*,<sup>7</sup> the first *continuous build* tool. I remember Mike Two<sup>8</sup> giving a late-night lecture about this at a 2001 XP Immersion. There’s no recording of that speech, but the story went something like this:

> *CruiseControl allows the checkin time to shrink down to a few minutes. Even the most minor change is quickly integrated into the mainline. CruiseControl watches the source code repository and kicks off a build every time any change is checked in. As part of the build, CruiseControl runs the majority of the automated tests for the system and then sends email to everyone on the team with the results.*
>
> “Bob broke the build.”

7. https://en.wikipedia.org/wiki/CruiseControl
8. http://wiki.c2.com/?MikeTwo

## The Cost of Cheating

There have been teams who, under the pressure of a deadline, have allowed the continuous build to remain in a failed state. This is a suicidal move. What happens is that everyone gets tired of the continuous barrage of failure emails from the continuous build server, so they remove the failing tests with the promise that they’ll go back and fix them “later.”

Of course, this causes the continuous build server to start sending success emails again. Everyone relaxes. The build is passing. And everyone forgets about the pile of failing tests that they set aside to be fixed “later.” And so a broken system gets deployed.

## Standup Meetings

Over the years, there has been a great deal of confusion about “The Daily Scrum” or the “Standup Meeting.” Let me cut through all that confusion now.

The following are true of the Standup Meeting:

- This meeting is optional. Many teams get by just fine without one.
- It can be less often than daily. Pick the schedule that makes sense to you.
- It should take ~10 minutes, even for large teams.
- This meeting follows a simple formula.

The basic idea is that the team members stand⁹ in a circle and answer three questions:

1. What did I do since the last meeting?
2. What will I do until the next meeting?
3. What is in my way?

⁹. This is why it’s called a “standup” meeting.
