
Deciding how much design to do before beginning full-scale coding and how much formality to use in documenting that design is hardly an exact science. The experience of the team, expected lifetime of the system, desired level of reliability, and size of project and team should all be considered. Table 5-2 summarizes how each of these factors influence the design approach.

**Table 5-2 — Design Formality and Level of Detail Needed**

| Factor | Level of Detail Needed in Design Before Construction | Documentation Formality |
|---|---|---|
| Design/construction team has deep experience in applications area. | Low Detail | Low Formality |
| Design/construction team has deep experience but is inexperienced in the applications area. | Medium Detail | Medium Formality |
| Design/construction team is inexperienced. | Medium to High Detail | Low-Medium Formality |
| Design/construction team has moderate-to-high turnover. | Medium Detail | — |
| Application is safety-critical. | High Detail | High Formality |
| Application is mission-critical. | Medium Detail | Medium-High Formality |
| Project is small. | Low Detail | Low Formality |
| Project is large. | Medium Detail | Medium Formality |
| Software is expected to have a short lifetime (weeks or months). | Low Detail | Low Formality |
| Software is expected to have a long lifetime (months or years). | Medium Detail | Medium Formality |

Two or more of these factors might come into play on any specific project, and in some cases the factors might provide contradictory advice. For example, you might have a highly experienced team working on safety critical software. In that case, you’d probably want to err on the side of the higher level of design detail and formality. In such cases, you’ll need to weigh the significance of each factor and make a judgment about what matters most.

If the level of design is left to each individual, then, when the design descends to the level of a task that you’ve done before or to a simple modification or extension of such a task, you’re probably ready to stop designing and begin coding.

If I can’t decide how deeply to investigate a design before I begin coding, I tend to err on the side of going into more detail. The biggest design errors arise from cases in which I thought I went far enough, but it later turns out that I didn’t go far enough to realize there were additional design challenges. In other words, the biggest design problems tend to arise not from areas I knew were difficult and created bad designs for, but from areas I thought were easy and didn’t create any designs for at all. I rarely encounter projects that are suffering from having done too much design work.

> > I've never met a human being who would want to read 17,000 pages of documentation, and if there was, I'd kill him to get him out of the room.
> > — *Joseph Costello*

On the other hand, occasionally I have seen projects that are suffering from too much design *documentation*. Gresham’s Law states that “programmed activity tends to drive out nonprogrammed activity” (Simon 1965). A premature rush to polish a design description is a good example of that law. I would rather see 80 percent of the design effort go into creating and exploring numerous design alternatives and 20 percent go into creating less polished documentation than to have 20 percent go into creating mediocre design alternatives and 80 percent go into polishing documentation of designs that are not very good.

## Capturing Your Design Work

The traditional approach to capturing design work is to write up the designs in a formal design document. However, you can capture designs in numerous alternative ways that work well on small projects, informal projects, or projects that need a lightweight way to record a design:

**Insert design documentation into the code itself**  Document key design decisions in code comments, typically in the file or class header. When you couple this approach with a documentation extractor like JavaDoc, this assures that design documentation will be readily available to a programmer working on a section of code, and it improves the chance that programmers will keep the design documentation reasonably up to date.

> > The bad news is that, in our opinion, we will never find the philosopher’s stone. We will never find a process that allows us to design software in a perfectly rational way. The good news is that we can fake it.
> > — *David Parnas and Paul Clements*

**Capture design discussions and decisions on a Wiki**  Have your design discussions in writing, on a project Wiki (that is, a collection of Web pages that can be edited easily by anyone on your project using a Web browser). This will capture your design discussions and decision automatically, albeit with the extra overhead of typing rather than talking. You can also use the Wiki to capture digital pictures to supplement the text discussion, links to websites that support the design decision, white papers, and other materials. This technique is especially useful if your development team is geographically distributed.

**Write e-mail summaries**  After a design discussion, adopt the practice of designating someone to write a summary of the discussion—especially what was decided—and send it to the project team. Archive a copy of the e-mail in the project’s public e-mail folder.

## Use a digital camera

One common barrier to documenting designs is the tedium of creating design drawings in some popular drawing tools. But the documentation choices are not limited to the two options of “capturing the design in a nicely formatted, formal notation” vs. “no design documentation at all.”

Taking pictures of whiteboard drawings with a digital camera and then embedding those pictures into traditional documents can be a low-effort way to get 80 percent of the benefit of saving design drawings by doing about 1 percent of the work required if you use a drawing tool.

## Save design flip charts

There’s no law that says your design documentation has to fit on standard letter-size paper. If you make your design drawings on large flip chart paper, you can simply archive the flip charts in a convenient location—or, better yet, post them on the walls around the project area so that people can easily refer to them and update them when needed.

## Use CRC (Class, Responsibility, Collaborator) cards

Another low-tech alternative for documenting designs is to use index cards. On each card, designers write a class name, responsibilities of the class, and collaborators (other classes that cooperate with the class). A design group then works with the cards until they’re satisfied that they’ve created a good design. At that point, you can simply save the cards for future reference. Index cards are cheap, unintimidating, and portable, and they encourage group interaction (Beck 1991).

## Create UML diagrams at appropriate levels of detail

One popular technique for diagramming designs is called Unified Modeling Language (UML), which is defined by the Object Management Group (Fowler 2004). Figure 5-6 earlier in this chapter was one example of a UML class diagram. UML provides a rich set of formalized representations for design entities and relationships. You can use informal versions of UML to explore and discuss design approaches. Start with minimal sketches and add detail only after you’ve zeroed in on a final design solution. Because UML is standardized, it supports common understanding in communicating design ideas and it can accelerate the process of considering design alternatives when working in a group.

These techniques can work in various combinations, so feel free to mix and match these approaches on a project-by-project basis or even within different areas of a single project.

## 5.5 Comments on Popular Methodologies

The history of design in software has been marked by fanatic advocates of wildly conflicting design approaches. When I published the first edition of Code Complete in the early 1990s, design zealots were advocating dotting every design i and crossing every design t before beginning coding. That recommendation didn’t make any sense.
