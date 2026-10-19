
black box has such a simple interface and such well-defined functionality that for any specific input you can accurately predict the corresponding output.

The concept of modularity is related to information hiding, encapsulation, and other design heuristics. But sometimes thinking about how to assemble a system from a set of black boxes provides insights that information hiding and encapsulation don’t, so the concept is worth having in your back pocket.

## Summary of Design Heuristics

> More alarming, the same programmer is quite capable of doing the same task himself in two or three ways, sometimes unconsciously, but quite often simply for a change, or to provide elegant variation.
> —A. R. Brown and W. A. Sampson

Here’s a summary of major design heuristics:

- Find Real-World Objects
- Form Consistent Abstractions
- Encapsulate Implementation Details
- Inherit When Possible
- Hide Secrets (Information Hiding)
- Identify Areas Likely to Change
- Keep Coupling Loose
- Look for Common Design Patterns

The following heuristics are sometimes useful too:

- Aim for Strong Cohesion
- Build Hierarchies
- Formalize Class Contracts
- Assign Responsibilities
- Design for Test
- Avoid Failure
- Choose Binding Time Consciously
- Make Central Points of Control
- Consider Using Brute Force
- Draw a Diagram
- Keep Your Design Modular

## Guidelines for Using Heuristics

Approaches to design in software can learn from approaches to design in other fields. One of the original books on heuristics in problem solving was G. Polya’s *How to Solve It* (1957). Polya’s generalized problem-solving approach focuses on problem solving in mathematics. Figure 5-10 is a summary of his approach, adapted from a similar summary in his book (emphases his).

1. **Understanding the Problem.** You have to *understand* the problem.

    *What is the unknown? What are the data? What is the condition?* Is it possible to satisfy the condition? Is the condition sufficient to determine the unknown? Or is it insufficient? Or redundant? Or contradictory?

    Draw a figure. Introduce suitable notation. Separate the various parts of the condition. Can you write them down?

2. **Devising a Plan.** Find the connection between the data and the unknown. You might be obliged to consider auxiliary problems if you can’t find an intermediate connection. You should eventually come up with a *plan* of the solution.

    *Have you seen the problem before?* Or have you seen the same problem in a slightly different form? *Do you know a related problem?* Do you know a theorem that could be useful?

    *Look at the unknown!* And try to think of a familiar problem having the same or a similar unknown. *Here is a problem related to yours and solved before.* *Can you use it?* Can you use its result? Can you use its method? Should you introduce some auxiliary element in order to make its use possible?

    Can you restate the problem? Can you restate it still differently? Go back to definitions.

    If you cannot solve the proposed problem, try to solve some related problem first. Can you imagine a more accessible related problem? A more general problem? A more special problem? An analogous problem? Can you solve a part of the problem? Keep only a part of the condition, drop the other part; how far is the unknown then determined, how can it vary? Can you derive something useful from the data? Can you think of other data appropriate for determining the unknown? Can you change the unknown or the data, or both if necessary, so that the new unknown and the new data are nearer to each other?

    Did you use all the data? Did you use the whole condition? Have you taken into account all essential notions involved in the problem?

3. **Carrying out the Plan.** *Carry out* your plan.

    Carrying out your plan of the solution, *check each step.* Can you see clearly that the step is correct? Can you prove that it’s correct?

4. **Looking Back.** Examine the solution.

    Can you *check the result?* Can you check the argument? Can you derive the result differently? Can you see it at a glance?

    Can you use the result, or the method, for some other problem?

Figure 5-10 G. Polya developed an approach to problem solving in mathematics that’s also useful in solving problems in software design (Polya 1957).

One of the most effective guidelines is not to get stuck on a single approach. If diagramming the design in UML isn’t working, write it in English. Write a short test program. Try a completely different approach. Think of a brute-force solution. Keep outlining and sketching with your pencil, and your brain will follow. If all else fails, walk away from the problem. Literally go for a walk, or think about something else before returning to the problem. If you’ve given it your best and are getting nowhere, putting it out of your mind for a time often produces results more quickly than sheer persistence can.

You don’t have to solve the whole design problem at once. If you get stuck, remember that a point needs to be decided but recognize that you don’t yet have enough information to resolve that specific issue. Why fight your way through the last 20 percent of the design when it will drop into place easily the next time through? Why make bad decisions based on limited experience with the design when you can make good decisions based on more experience with it later? Some people are uncomfortable if they don’t come to closure after a design cycle, but after you have created a few designs without resolving issues prematurely, it will seem natural to leave issues unresolved until you have more information (Zahniser 1992, Beck 2000).

## 5.4 Design Practices

The preceding section focused on heuristics related to design attributes—what you want the completed design to look like. This section describes design practice heuristics, steps you can take that often produce good results.

### Iterate

You might have had an experience in which you learned so much from writing a program that you wished you could write it again, armed with the insights you gained from writing it the first time. The same phenomenon applies to design, but the design cycles are shorter and the effects downstream are bigger, so you can afford to whirl through the design loop a few times.

![](img/649c8eee28c38ca1e062691e45dc9883_146_0.png)

Design is an iterative process. You don’t usually go from point A only to point B; you go from point A to point B and back to point A.

As you cycle through candidate designs and try different approaches, you’ll look at both high-level and low-level views. The big picture you get from working with high-level issues will help you to put the low-level details in perspective. The details you get from working with low-level issues will provide a foundation in solid reality for the high-level decisions. The tug and pull between top-level and bottom-level considerations is a healthy dynamic; it creates a stressed structure that’s more stable than one built wholly from the top down or the bottom up.

Many programmers—many people, for that matter—have trouble ranging between high-level and low-level considerations. Switching from one view of a system to another is mentally strenuous, but it’s essential to creating effective designs. For entertaining exercises to enhance your mental flexibility, read Conceptual Blockbusting (Adams 2001), described in the “Additional Resources” section at the end of the chapter.

Cross-Reference Refactoring is a safe way to try different alternatives in code. For more on this, see Chapter 24, "Refactoring."

When you come up with a first design attempt that seems good enough, don’t stop! The second attempt is nearly always better than the first, and you learn things on each attempt that can improve your overall design. After trying a thousand different materials for a light bulb filament with no success, Thomas Edison was reportedly asked if he felt his time had been wasted since he had discovered nothing. “Nonsense,” Edison is supposed to have replied. “I have discovered a thousand things that don’t work.” In many cases, solving the problem with one approach will produce insights that will enable you to solve the problem using another approach that’s even better.

### Divide and Conquer

As Edsger Dijkstra pointed out, no one’s skull is big enough to contain all the details of a complex program, and that applies just as well to design. Divide the program into different areas of concern, and then tackle each of those areas individually. If you run into a dead end in one of the areas, iterate!

Incremental refinement is a powerful tool for managing complexity. As Polya recommended in mathematical problem solving, understand the problem, devise a plan, carry out the plan, and then look back to see how you did (Polya 1957).

### Top-Down and Bottom-Up Design Approaches

“Top down” and “bottom up” might have an old-fashioned sound, but they provide valuable insight into the creation of object-oriented designs. Top-down design begins at a high level of abstraction. You define base classes or other nonspecific design elements. As you develop the design, you increase the level of detail, identifying derived classes, collaborating classes, and other detailed design elements.

Bottom-up design starts with specifics and works toward generalities. It typically begins by identifying concrete objects and then generalizes aggregations of objects and base classes from those specifics.

Some people argue vehemently that starting with generalities and working toward specifics is best, and some argue that you can’t really identify general design principles until you’ve worked out the significant details. Here are the arguments on both sides.
