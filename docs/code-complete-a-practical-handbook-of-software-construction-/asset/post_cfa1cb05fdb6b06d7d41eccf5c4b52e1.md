
In other ways, performance issues have hardly changed at all. People writing desktop applications may not need this information, but people writing software for embedded systems, real-time systems, and other systems with strict speed or space restrictions can still benefit from it.

The need to measure the impact of each and every attempt at code tuning has been a constant since Donald Knuth published his study of Fortran programs in 1971. According to the measurements in this chapter, the effect of any specific optimization is actually less predictable than it was 10 years ago. The effect of each code tuning is affected by the programming language, compiler, compiler version, code libraries, library versions, and compiler settings, among other things.

Code tuning invariably involves tradeoffs among complexity, readability, simplicity, and maintainability on the one hand and a desire to improve performance on the other. It introduces a high degree of maintenance overhead because of all the reprofiling that’s required.

I have found that insisting on measurable improvement is a good way to resist the temptation to optimize prematurely and a good way to enforce a bias toward clear, straightforward code. If an optimization is important enough to haul out the profiler and measure the optimization’s effect, then it’s probably important enough to allow—as long as it works. But if an optimization isn’t important enough to haul out the profiling machinery, it isn’t important enough to degrade readability, maintainability, and other code characteristics. The impact of unmeasured code tuning on performance is speculative at best, whereas the impact on readability is as certain as it is detrimental.

## Additional Resources

cc2e.com/2679

My favorite reference on code tuning is Writing Efficient Programs (Bentley, Englewood Cliffs, NJ: Prentice Hall, 1982). The book is out of print but worth reading if you can find it. It’s an expert treatment of code tuning, broadly considered. Bentley describes techniques that trade time for space and space for time. He provides several examples of redesigning data types to reduce both space and time. His approach is a little more anecdotal than the one taken here, and his anecdotes are interesting. He takes a few routines through several optimization steps so that you can see the effects of first, second, and third attempts on a single problem. Bentley strolls through the primary contents of the book in 135 pages. The book has an unusually high signal-to-noise ratio—it’s one of the rare gems that every practicing programmer should own.

Appendix 4 of Bentley’s Programming Pearls, 2d ed. (Boston, MA: Addison-Wesley, 2000) contains a summary of the code-tuning rules from his earlier book.

You can also find a full array of technology-specific optimization books. Several are listed below, and the Web link to the left contains an up-to-date list.

Booth, Rick. *Inner Loops: A Sourcebook for Fast 32-bit Software Development*. Boston, MA: Addison-Wesley, 1997.

Gerber, Richard. *Software Optimization Cookbook: High-Performance Recipes for the Intel Architecture*. Intel Press, 2002.

Hasan, Jeffrey and Kenneth Tu. *Performance Tuning and Optimizing ASP.NET Applications*. Berkeley, CA: Apress, 2003.

Killelea, Patrick. *Web Performance Tuning*, 2d ed. Sebastopol, CA: O’Reilly & Associates, 2002.

Larman, Craig and Rhett Guthrie. *Java 2 Performance and Idiom Guide*. Englewood Cliffs, NJ: Prentice Hall, 2000.

Shirazi, Jack. *Java Performance Tuning*. Sebastopol, CA: O’Reilly & Associates, 2000.

Wilson, Steve and Jeff Kesselman. *Java Platform Performance: Strategies and Tactics*. Boston, MA: Addison-Wesley, 2000.

## Key Points

- Results of optimizations vary widely with different languages, compilers, and environments. Without measuring each specific optimization, you’ll have no idea whether it will help or hurt your program.
- The first optimization is often not the best. Even after you find a good one, keep looking for one that’s better.
- Code tuning is a little like nuclear energy. It’s a controversial, emotional topic. Some people think it’s so detrimental to reliability and maintainability that they won’t do it at all. Others think that with proper safeguards, it’s beneficial. If you decide to use the techniques in this chapter, apply them with care.

## Part VI

## System Considerations

- In this part:
- Chapter 27: How Program Size Affects Construction .................649
- Chapter 28: Managing Construction .................661
- Chapter 29: Integration .................689
- Chapter 30: Programming Tools .................709

## Chapter 27

## How Program Size Affects Construction

## Contents

- 27.1 Communication and Size: page 650
- 27.2 Range of Project Sizes: page 651
- 27.3 Effect of Project Size on Errors: page 651
- 27.4 Effect of Project Size on Productivity: page 653
- 27.5 Effect of Project Size on Development Activities: page 654

## Related Topics

- Prerequisites to construction: Chapter 3
- Determining the kind of software you’re working on: Section 3.2
- Managing construction: Chapter 28

Scaling up in software development isn’t a simple matter of taking a small project and making each part of it bigger. Suppose you wrote the 25,000-line Gigatron software package in 20 staff-months and found 500 errors in field testing. Suppose Gigatron 1.0 is successful, as is Gigatron 2.0, and you start work on the Gigatron Deluxe, a greatly enhanced version of the program that’s expected to be 250,000 lines of code.

Even though it’s 10 times as large as the original Gigatron, the Gigatron Deluxe won’t take 10 times the effort to develop; it’ll take 30 times the effort. Moreover, 30 times the total effort doesn’t imply 30 times as much construction. It probably implies 25 times as much construction and 40 times as much architecture and system testing. You won’t have 10 times as many errors either; you’ll have 15 times as many—or more.

If you’ve been accustomed to working on small projects, your first medium-to-large project can rage riotously out of control, becoming an uncontrollable beast instead of the pleasant success you had envisioned. This chapter tells you what kind of beast to expect and where to find the whip and chair to tame it. In contrast, if you’re accustomed to working on large projects, you might use approaches that are too formal on a small project. This chapter describes how you can economize to keep a small project from toppling under the weight of its own overhead.

### 27.1 Communication and Size

If you’re the only person on a project, the only communication path is between you and the customer, unless you count the path across your corpus callosum, the path that connects the left side of your brain to the right. As the number of people on a project increases, the number of communication paths increases, too. The number doesn’t increase additively as the number of people increases. It increases multiplicatively, proportionally to the square of the number of people, as illustrated in Figure 27-1.

![](img/649c8eee28c38ca1e062691e45dc9883_686_0.png)

Figure 27-1 The number of communication paths increases proportionate to the square of the number of people on the team.

![](img/649c8eee28c38ca1e062691e45dc9883_686_1.png)

As you can see, a two-person project has only one path of communication. A five-person project has 10 paths. A ten-person project has 45 paths, assuming that every person talks to every other person. The 10 percent of projects that have 50 or more programmers have at least 1,200 potential paths. The more communication paths you have, the more time you spend communicating and the more opportunities are created for communication mistakes. Larger-size projects demand organizational techniques that streamline communication or limit it in a sensible way.

The typical approach taken to streamlining communication is to formalize it in documents. Instead of having 50 people talk to each other in every conceivable combination, 50 people read and write documents. Some are text documents; some are graphic. Some are printed on paper; others are kept in electronic form.
