# 9.1. COMMON THEMES

# 9.1.1. Development methods

Rapid prototyping

The proposal for the project envisaged that development of demonstrators would proceed by means of 'rapid prototyping'. However, in 1984 this idea was ill-defined and there was little other anecdote to indicate what constituted development by rapid prototyping. We therefore spent some time at the beginning of the project trying small-scale experiments and debating the merits of what we were doing. For the purpose of experimentation, we took rapid prototyping to be a development method which dispensed with formal design methods, designing by building and trying alternative solutions, by means of a 'prototype' rather than by written documentation, and using highly interactive programming tools.

It quickly became clear that 'rapid' is an imprecise and relative term. Some thought a cycle of design, implementation and evaluation over the course of a year was 'rapid'; others expected a cycle to be completed in a week. Our experience showed that there were major disadvantages associated with rapid prototyping:

+   1. One motive for rapid prototyping was that it allegedly allowed the designer to explore the design space quickly and then select the best from a range of possible designs. In fact, although we were using probably the best prototyping software environment available (InterDisp-D), construction of a single prototype to the point where it could be evaluated took months of work. This meant that major design decisions were made by default — the first design to prototype became the only one to be examined and therefore the one to be adopted.

+   2. It is impossible to design and build prototypes of very large and complex systems rapidly, because they are so large. The only practical method is to decompose the system into much smaller modules and build prototypes of these. However, if a large number of modules are undergoing rapid evolution, the tasks of defining and maintaining common interfaces, of integration, and of promoting a common design 'philosophy' throughout becomes very difficult.

While we became sceptical about the value of 'rapid prototyping' itself, the alternative against which it has often been counterposted — design through the use of formal methods -- was also not seen as ideal. We were building systems whose precise functionality could not easily be predicted in advance. In addition, current methods for the formal specification of interfaces and, in particular, for human-computer interaction, were rudimentary and largely untried.

Combining rapid prototyping and specification