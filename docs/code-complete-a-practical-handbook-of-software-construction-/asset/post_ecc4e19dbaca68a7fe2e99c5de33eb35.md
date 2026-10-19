
## Chapter 33
## Personal Character
### Contents
- 33.1 Isn’t Personal Character Off the Topic?: page 820
- 33.2 Intelligence and Humility: page 821
- 33.3 Curiosity: page 822
- 33.4 Intellectual Honesty: page 826
- 33.5 Communication and Cooperation: page 828
- 33.6 Creativity and Discipline: page 829
- 33.7 Laziness: page 830
- 33.8 Characteristics That Don’t Matter As Much As You Might Think: page 830
- 33.9 Habits: page 833

### Related Topics
- Themes in software craftsmanship: Chapter 34
- Complexity: Sections 5.2 and 19.6

Personal character has received a rare degree of attention in software development. Ever since Edsger Dijkstra’s landmark 1965 article, “Programming Considered as a Human Activity,” programmer character has been regarded as a legitimate and fruitful area of inquiry. Titles such as *The Psychology of Bridge Construction* and “Exploratory Experiments in Attorney Behavior” might seem absurd, but in the computer field *The Psychology of Computer Programming*, “Exploratory Experiments in Programmer Behavior,” and similar titles are classics.

Engineers in every discipline learn the limits of the tools and materials they work with. If you’re an electrical engineer, you know the conductivity of various metals and a hundred ways to use a voltmeter. If you’re a structural engineer, you know the load-bearing properties of wood, concrete, and steel.

If you’re a software engineer, your basic building material is human intellect and your primary tool is you. Rather than designing a structure to the last detail and then handing the blueprints to someone else for construction, you know that once you’ve designed a piece of software to the last detail, it’s done. The whole job of programming is building air castles—it’s one of the most purely mental activities you can do.

### 33.2 Intelligence and Humility

> We become authorities and experts in the practical and scientific spheres by so many separate acts and hours of work. If a person keeps faithfully busy each hour of the working day, he can count on waking up some morning to find himself one of the competent ones of his generation.
> 
> —William James

Intelligence doesn’t seem like an aspect of personal character, and it isn’t. Coincidentally, great intelligence is only loosely connected to being a good programmer.

What? You don’t have to be superintelligent?

No, you don’t. Nobody is really smart enough to program computers. Fully understanding an average program requires an almost limitless capacity to absorb details and an equal capacity to comprehend them all at the same time. The way you focus your intelligence is more important than how much intelligence you have.

As Chapter 5 (“Design in Construction”) mentioned, at the 1972 Turing Award Lecture, Edsger Dijkstra delivered a paper titled “The Humble Programmer.” He argued that most of programming is an attempt to compensate for the strictly limited size of our skulls. The people who are best at programming are the people who realize how small their brains are. They are humble. The people who are the worst at programming are the people who refuse to accept the fact that their brains aren’t equal to the task. Their egos keep them from being great programmers. The more you learn to compensate for your small brain, the better a programmer you’ll be. The more humble you are, the faster you’ll improve.

The purpose of many good programming practices is to reduce the load on your gray cells. Here are a few examples:

- The point of “decomposing” a system is to make it simpler to understand. (See ”Levels of Design” in Section 5.2 for more details.)
- Conducting reviews, inspections, and tests is a way of compensating for anticipated human fallibilities. These review techniques originated as part of “egoless programming” (Weinberg 1998). If you never made mistakes, you wouldn’t need to review your software. But you know that your intellectual capacity is limited, so you augment it with someone else’s.
- Keeping routines short reduces the load on your brain.
- Writing programs in terms of the problem domain rather than in terms of low-level implementation details reduces your mental workload.
- Using conventions of all sorts frees your brain from the relatively mundane aspects of programming, which offer little payback.

You might think that the high road would be to develop better mental abilities so that you wouldn’t need these programming crutches. You might think that a programmer who uses mental crutches is taking the low road. Empirically, however, it’s been shown that humble programmers who compensate for their fallibilities write code that’s easier for themselves and others to understand and that has fewer errors. The real low road is the road of errors and delayed schedules.

What if the short program shows that the feature doesn’t work the way you want it to? That’s what you wanted to find out. Better to find it out in a small program than a large one. One key to effective programming is learning to make mistakes quickly, learning from them each time. Making a mistake is no sin. Failing to learn from a mistake is.

**Read about problem solving** Problem solving is the core activity in building computer software. Herbert Simon reported a series of experiments on human problem solving. They found that human beings don’t always discover clever problem-solving strategies themselves, even though the same strategies could readily be taught to the same people (Simon 1996). The implication is that even if you want to reinvent the wheel, you can’t count on success. You might reinvent the square instead.

**Analyze and plan before you act** You’ll find that there’s a tension between analysis and action. At some point you have to quit gathering data and act. The problem for most programmers, however, isn’t an excess of analysis. The pendulum is currently so far on the “acting” side of the arc that you can wait until it’s at least partway to the middle before worrying about getting stuck on the “analysis-paralysis” side.

**Learn about successful projects** One especially good way to learn about programming is to study the work of the great programmers. Jon Bentley thinks that you should be able to sit down with a glass of brandy and a good cigar and read a program the way you would a good novel. That might not be as far-fetched as it sounds. Most people wouldn’t want to use their recreational time to scrutinize a 500-page source listing, but many people would enjoy studying a high-level design and dipping into more detailed source listings for selected areas.

The software-engineering field makes extraordinarily limited use of examples of past successes and failures. If you were interested in architecture, you’d study the drawings of Louis Sullivan, Frank Lloyd Wright, and I. M. Pei. You’d probably visit some of their buildings. If you were interested in structural engineering, you’d study the Brooklyn Bridge; the Tacoma Narrows Bridge; and a variety of other concrete, steel, and wood structures. You would study examples of successes and failures in your field.

Thomas Kuhn points out that a part of any mature science is a set of solved problems that are commonly recognized as examples of good work in the field and that serve as examples for future work (Kuhn 1996). Software engineering is only beginning to mature to this level. In 1990, the Computer Science and Technology Board concluded that there were few documented case studies of either successes or failures in the software field (CSTB 1990).

An article in the *Communications of the ACM* argued for learning from case studies of programming problems (Linn and Clancy 1992). The fact that someone has to argue

**Further Reading** A great book that teaches problem solving is James Adams’s *Conceptual Blockbusting* (2001).
