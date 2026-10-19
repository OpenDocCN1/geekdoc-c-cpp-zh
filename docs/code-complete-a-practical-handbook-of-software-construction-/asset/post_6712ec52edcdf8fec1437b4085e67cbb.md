
## 2.3 Common Software Metaphors

A confusing abundance of metaphors has grown up around software development. David Gries says writing software is a science (1981). Donald Knuth says it’s an art (1998). Watts Humphrey says it’s a process (1989). P. J. Plauger and Kent Beck say it’s like driving a car, although they draw nearly opposite conclusions (Plauger 1993, Beck 2000). Alistair Cockburn says it’s a game (2002). Eric Raymond says it’s like a bazaar (2000). Andy Hunt and Dave Thomas say it’s like gardening. Paul Heckel says it’s like filming Snow White and the Seven Dwarfs (1994). Fred Brooks says that it’s like farming, hunting werewolves, or drowning with dinosaurs in a tar pit (1995). Which are the best metaphors?

## Software Penmanship: Writing Code

The most primitive metaphor for software development grows out of the expression “writing code.” The writing metaphor suggests that developing a program is like writing a casual letter—you sit down with pen, ink, and paper and write it from start to finish. It doesn’t require any formal planning, and you figure out what you want to say as you go.

Many ideas derive from the writing metaphor. Jon Bentley says you should be able to sit down by the fire with a glass of brandy, a good cigar, and your favorite hunting dog to enjoy a “literate program” the way you would a good novel. Brian Kernighan and P. J. Plauger named their programming-style book The Elements of Programming Style (1978) after the writing-style book The Elements of Style (Strunk and White 2000). Programmers often talk about “program readability.”

![](img/649c8eee28c38ca1e062691e45dc9883_49_0.png)

For an individual’s work or for small-scale projects, the letter-writing metaphor works adequately, but for other purposes it leaves the party early—it doesn’t describe software development fully or adequately. Writing is usually a one-person activity, whereas a software project will most likely involve many people with many different responsibilities. When you finish writing a letter, you stuff it into an envelope and mail it. You can’t change it anymore, and for all intents and purposes it’s complete. Software isn’t as difficult to change and is hardly ever fully complete. As much as 90 percent of the development effort on a typical software system comes after its initial release, with two-thirds being typical (Pigoski 1997). In writing, a high premium is placed on originality. In software construction, trying to create truly original work is often less effective than focusing on the reuse of design ideas, code, and test cases from previous projects. In short, the writing metaphor implies a software-development process that’s too simple and rigid to be healthy.

> Plan to throw one away; you will, anyhow.
> —Fred Brooks

> If you plan to throw one away, you will throw away two.
> —Craig Zerouni

Unfortunately, the letter-writing metaphor has been perpetuated by one of the most popular software books on the planet, Fred Brooks’s The Mythical Man-Month (Brooks 1995). Brooks says, “Plan to throw one away; you will, anyhow.” This conjures up an image of a pile of half-written drafts thrown into a wastebasket, as shown in Figure 2-1.

![](img/649c8eee28c38ca1e062691e45dc9883_50_0.png)

Figure 2-1 The letter-writing metaphor suggests that the software process relies on expensive trial and error rather than careful planning and design.

Planning to throw one away might be practical when you’re writing a polite how-do-you-do to your aunt. But extending the metaphor of “writing” software to a plan to throw one away is poor advice for software development, where a major system already costs as much as a 10-story office building or an ocean liner. It’s easy to grab the brass ring if you can afford to sit on your favorite wooden pony for an unlimited number of spins around the carousel. The trick is to get it the first time around—or to take several chances when they’re cheapest. Other metaphors better illuminate ways of attaining such goals.

## Software Farming: Growing a System

In contrast to the rigid writing metaphor, some software developers say you should envision creating software as something like planting seeds and growing crops. You design a piece, code a piece, test a piece, and add it to the system a little bit at a time. By taking small steps, you minimize the trouble you can get into at any one time.

![](img/649c8eee28c38ca1e062691e45dc9883_50_1.png)

Sometimes a good technique is described with a bad metaphor. In such cases, try to keep the technique and come up with a better metaphor. In this case, the incremental technique is valuable, but the farming metaphor is terrible.

Further Reading For an illustration of a different farming metaphor, one that’s applied to software maintenance, see the chapter “On the Origins of Designer Intuition” in Rethinking Systems Analysis and Design (Weinberg 1988).

The idea of doing a little bit at a time might bear some resemblance to the way crops grow, but the farming analogy is weak and uninformative, and it’s easy to replace with the better metaphors described in the following sections. It’s hard to extend the farming metaphor beyond the simple idea of doing things a little bit at a time. If you buy into the farming metaphor, imagined in Figure 2-2, you might find yourself talking about fertilizing the system plan, thinning the detailed design, increasing code yields through effective land management, and harvesting the code itself. You’ll talk about

rotating in a crop of C++ instead of barley, of letting the land rest for a year to increase the supply of nitrogen in the hard disk.

The weakness in the software-farming metaphor is its suggestion that you don’t have any direct control over how the software develops. You plant the code seeds in the spring. Farmer’s Almanac and the Great Pumpkin willing, you’ll have a bumper crop of code in the fall.

![](img/649c8eee28c38ca1e062691e45dc9883_51_0.png)

Figure 2-2 It’s hard to extend the farming metaphor to software development appropriately.

## Software Oyster Farming: System Accretion

Sometimes people talk about growing software when they really mean software accretion. The two metaphors are closely related, but software accretion is the more insightful image. “Accretion,” in case you don’t have a dictionary handy, means any growth or increase in size by a gradual external addition or inclusion. Accretion describes the way an oyster makes a pearl, by gradually adding small amounts of calcium carbonate. In geology, “accretion” means a slow addition to land by the deposit of waterborne sediment. In legal terms, “accretion” means an increase of land along the shores of a body of water by the deposit of waterborne sediment.

Cross-Reference For details on how to apply incremental strategies to system integration, see Section 29.2, “Integration Frequency—Phased or Incremental?”

This doesn’t mean that you have to learn how to make code out of waterborne sediment; it means that you have to learn how to add to your software systems a small amount at a time. Other words closely related to accretion are “incremental,” “iterative,” “adaptive,” and “evolutionary.” Incremental designing, building, and testing are some of the most powerful software-development concepts available.

In incremental development, you first make the simplest possible version of the system that will run. It doesn’t have to accept realistic input, it doesn’t have to perform realistic manipulations on data, it doesn’t have to produce realistic output—it just has to be a skeleton strong enough to hold the real system as it’s developed. It might call dummy classes for each of the basic functions you have identified. This basic beginning is like the oyster’s beginning a pearl with a small grain of sand.

After you’ve formed the skeleton, little by little you lay on the muscle and skin. You change each of the dummy classes to real classes. Instead of having your program
