
As you work with the system, you can begin moving code across the “real world interface” into a more organized ideal world. When you begin working with a legacy system, the poorly written legacy code might make up nearly all the system. One policy that works well is that anytime you touch a section of messy code, you are required to bring it up to current coding standards, give it clear variable names, and so on—effectively moving it into the ideal world. Over time this can provide for a rapid improvement in a code base, as shown in Figure 24-3.

![](img/649c8eee28c38ca1e062691e45dc9883_620_0.png)

**Figure 24-3** One strategy for improving production code is to refactor poorly written legacy code as you touch it, so as to move it to the other side of the “interface to the messy real world.”

**CHECKLIST: Refactoring Safely**

- Is each change part of a systematic change strategy?
- Did you save the code you started with before beginning refactoring?
- Are you keeping each refactoring small?
- Are you doing refactorings one at a time?
- Have you made a list of steps you intend to take during your refactoring?
- Do you have a parking lot so that you can remember ideas that occur to you mid-refactoring?
- Have you retested after each refactoring?
- Have changes been reviewed if they are complicated or if they affect mission-critical code?
- Have you considered the riskiness of the specific refactoring and adjusted your approach accordingly?
- Does the change enhance the program’s internal quality rather than degrade it?
- Have you avoided using refactoring as a cover for code-and-fix or as an excuse for not rewriting bad code?

### Additional Resources

cc2e.com/2464

The process of refactoring has a lot in common with the process of fixing defects. For more on fixing defects, see Section 23.3, “Fixing a Defect.” The risks associated with refactoring are similar to the risks associated with code tuning. For more on managing code-tuning risks, see Section 25.6, “Summary of the Approach to Code Tuning.”

Fowler, Martin. *Refactoring: Improving the Design of Existing Code.* Reading, MA: Addison-Wesley, 1999. This is the definitive guide to refactoring. It contains detailed discussions of many of the specific refactorings summarized in this chapter, as well as a handful of other refactorings not summarized here. Fowler provides numerous code samples to illustrate how each refactoring is performed step by step.

### Key Points

- Program changes are a fact of life both during initial development and after initial release.
- Software can either improve or degrade as it’s changed. The Cardinal Rule of Software Evolution is that internal quality should improve with code evolution.
- One key to success in refactoring is learning to pay attention to the numerous warning signs or smells that indicate a need to refactor.
- Another key to refactoring success is learning numerous specific refactorings.
- A final key to success is having a strategy for refactoring safely. Some refactoring approaches are better than others.
- Refactoring during development is the best chance you’ll get to improve your program, to make all the changes you’ll wish you’d made the first time. Take advantage of these opportunities during development!

## Chapter 25: Code-Tuning Strategies

### Contents

- 25.1 Performance Overview: page 588
- 25.2 Introduction to Code Tuning: page 591
- 25.3 Kinds of Fat and Molasses: page 597
- 25.4 Measurement: page 603
- 25.5 Iteration: page 605
- 25.6 Summary of the Approach to Code Tuning: page 606

### Related Topics

- Code-tuning techniques: Chapter 26
- Software architecture: Section 3.5

This chapter discusses the question of performance tuning—historically, a controversial issue. Computer resources were severely limited in the 1960s, and efficiency was a paramount concern. As computers became more powerful in the 1970s, programmers realized how much their focus on performance had hurt readability and maintainability and code tuning received less attention. The return of performance limitations with the microcomputer revolution of the 1980s again brought efficiency to the fore, which then waned throughout the 1990s. In the 2000s, memory limitations in embedded software for devices such as telephones and PDAs and the execution time of interpreted code have once again made efficiency a key topic.

You can address performance concerns at two levels: strategic and tactical. This chapter addresses strategic performance issues: what performance is, how important it is, and the general approach to achieving it. If you already have a good grip on performance strategies and are looking for specific code-level techniques that improve performance, move on to Chapter 26, “Code-Tuning Techniques.” Before you begin any major performance work, however, at least skim the information in this chapter so that you don’t waste time optimizing when you should be doing other kinds of work.

### 25.1 Performance Overview

Code tuning is one way of improving a program’s performance. You can often find other ways to improve performance more—and in less time and with less harm to the code—than by code tuning. This section describes the options.

**Quality Characteristics and Performance**

> More computing sins are committed in the name of efficiency (without necessarily achieving it) than for any other single reason— including blind stupidity.
> —W. A. Wulf

Some people look at the world through rose-colored glasses. Programmers like you and me tend to look at the world through code-colored glasses. We assume that the better we make the code, the more our clients and customers will like our software.

This point of view might have a mailing address somewhere in reality, but it doesn’t have a street number and it certainly doesn’t own any real estate. Users are more interested in tangible program characteristics than they are in code quality. Sometimes users are interested in raw performance, but only when it affects their work. Users tend to be more interested in program throughput than raw performance. Delivering software on time, providing a clean user interface, and avoiding downtime are often more significant.

Here’s an illustration. I take at least 50 pictures a week on my digital camera. To upload the pictures to my computer, the software that came with the camera requires me to select each picture one by one, viewing them in a window that shows only six pictures at a time. Uploading 50 pictures is a tedious process that requires dozens of mouse clicks and lots of navigation through the six-picture window. After putting up with this for a few months, I bought a memory-card reader that plugs directly into my computer and that my computer thinks is a disk drive. Now I can use Windows Explorer to copy the pictures to my computer. What used to take dozens of mouse clicks and lots of waiting now requires about two mouse clicks, a Ctrl+A, and a drag and drop. I really don’t care whether the memory card reader transfers each file in half the time or twice the time as the other software, because my throughput is faster. Regardless of whether the memory card reader’s code is faster or slower, its performance is better.

![](img/649c8eee28c38ca1e062691e45dc9883_624_0.png)

Performance is only loosely related to code speed. To the extent that you work on your code’s speed, you’re not working on other quality characteristics. Be wary of sacrificing other characteristics to make your code faster. Your work on speed might hurt overall performance rather than help it.

**Performance and Code Tuning**

Once you’ve chosen efficiency as a priority, whether its emphasis is on speed or on size, you should consider several options before choosing to improve either speed or size at the code level. Think about efficiency from each of these viewpoints:
