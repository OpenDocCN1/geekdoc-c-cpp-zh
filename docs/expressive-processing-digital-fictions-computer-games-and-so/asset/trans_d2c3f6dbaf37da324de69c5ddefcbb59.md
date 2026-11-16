

- 1. 简要讨论可参见《Twisty Little Passages》（Montfort 2003, 126–127）。更详细的内容，包括源代码示例，可参见“Zork：一款电脑化奇幻模拟游戏”（Lebling, Blank, and Anderson 1979）。

- 2. 这是 Java 平台虚拟机所采用相同策略的早期商业实例。

wasn’t necessary for me to do so. Though Basic was part of the built-in, read-only memory of the Apple II, by working in it I wasn’t functioning in the essential language of the computer. Instead, I was using an authoring system, created to make it easier to develop certain kinds of software. The authors of Zork were using a completely different system, designed to make their sort of software easier to create.

In fact, the authors of Infocom’s popular interactive fiction titles employed several layers of software I didn’t begin to imagine. Rather than use the versions of Basic (or some other language) specific to the various personal computers of the 1970s and 1980s, their code was written to run on a “virtual machine”—versions of which they created for each major platform.2 Further, the essential elements for supporting gameplay (interpreting text typed by the audience, simulating a virtual space, managing manipulatable objects, and so on) were abstracted into a kind of game engine. Each author (or set of collaborators) creating an Infocom fiction was mainly occupied creating the specific text and behaviors for the places, objects, and characters in that fiction—rather than starting from scratch, as I imagined.

To put it another way, the fact that I didn’t recognize Basic as a set of authoring tools was only the tip of the iceberg. More generally, I didn’t recognize that most digital media creation takes place within systems specially designed to support particular types of authoring tasks, and that these systems are in turn supported by layers of further systems. Elements that look like system processes on one level (e.g., a series of commands in a programming language) can come to look like data on another level (e.g., a compiler using its processes to translate those commands for another system). The power afforded by this fact allows for the crafting of special-purpose authoring environments—from game engines to interactive animation software—that can make some tasks much easier and others impossible.

## 创作故事

When story-generation systems are thought of as media rather than simulations of human intelligence, issues of authoring come to the fore. Creating a successful story-generation system requires thinking in terms of the audience's surface experience and also in terms of the structures presented for authoring the elements of that experience—what Michael Mateas calls the system's authorial and interpretive *affordances*. This chapter examines three influential story-generation systems both as authored artifacts and systems for authoring, as well as related concepts such as Mateas's.

Like any digital media system, a story-generation system has one simple requirement: along some dimension(s), the system should offer an advantage over other solutions. For example, Infocom sought to create interactive story experiences for broad audiences. Implementing a software system had the advantage of making this possible, given that it was impossible for Infocom authors to make personal visits to the homes and workplaces of thousands of simultaneous players. On a more serious note, implementing a virtual machine made it easier for Infocom titles to reach audiences playing on the wide variety of 1980s-era personal computing platforms, as compared with “porting” the games to each operating system.

Beyond this simple litmus test, the sorts of story systems considered in this chapter also have two further requirements. First, they must be expressive and controllable, so that their underlying models effectively shape the audience experience. Without this, much of the effort involved in developing their fictional models is arguably wasted. At the same time, these systems must also be *authorable*—not departing so far from the skills and expectations of traditional authors that developing material for them is unrealistically onerous and unable to draw on our vast body of experience in media authoring. Balancing these two requirements can be a challenge.

Looking at this chapter's example systems also foregrounds another key difference between the practices of artificial intelligence (AI) and digital media. In AI, as in many areas of computer science, a system does not need to be completed in order to be influential. Computer science rewards the creation of innovative processes and mostly considers data the province of other fields. This results in a significant incentive against actually completing the authoring work for story-generation systems. Completing the data is time-consuming work with little direct reward, especially for systems that are not well designed for authorability.

Unfortunately, unfinished systems provide substantially less valuable results for both fields, because neither their processes for story generation nor their support for authoring are fully tested. Yet unfinished systems remain worth examining, because it is the only way to gain insight from the creative work performed in many computer science projects. This is visible in two of the systems discussed in this chapter: *Universe* and *Brutus*. This chapter's final example, *Terminal Time*, takes the next step—both departing from an exclusive disciplinary identification with computer science and (perhaps as a consequence) creating a completed system.

### Universe

Michael Lebowitz began work on Universe around the same time that Scott Turner started his work on Minstrel, and the two systems bear a number of similarities. Both focus on the importance of authorial actions rather than simply character actions. Both emerge from the scruffy artificial intelligence tradition—Lebowitz had recently written his dissertation at Yale under Roger Schank's supervision, contributing to Schank's model of dynamic memory, especially in relation to story understanding. Descriptions of both also emphasize the importance of the “point” or “theme” that the system is working to communicate through each act of generation (Lebowitz 1984, 175).

But in addition to its similarities with Minstrel, Universe also has an unusual feature in common with Tale-Spin. Just as the most famous stories attributed to Tale-Spin are actually hand transcriptions of early errors, the most famous story attributed to Universe was a somewhat more tenuous connection to the project than one might assume.

Here is the story:

Liz was told to Tony: Neither loved the other, and, indeed, Liz was in love with Neil. However, unknown to either Tony or Neil, Stephano, Tony's father, who wanted Liz to produce a grandson for him, threatened Liz that if she left Tony, he would kill Neil. Liz told Neil that she did not love him, that she was still in love with Tony, and that he should forget about her. Eventually, Neil was convinced and he married Marie. Later, when Liz was finally

- 3. Lebowitz's work on Universe was carried out while a faculty member at Columbia University, during which time (according to the acknowledgments in Lebowitz's 1984 and 1987 papers) work by Paula Langer and Doron Shalmon...

- 4. Lebowitz's dissertation “Generalization and Memory in an Integrated Understanding System,” filed December 1980.

Notes continued at end of this chapter.

- 5. These authors include Marie-Laure Ryan (1992, 246) and Janet Murray (1997, 201).

- 6. “Memory organization points” are also known as “memory organization packages.”

Though a number of prominent authors provide this as an example of Universe’s output, in fact this is a summarization of a plot from Days of Our Lives.5 It appears in a paper about Universe as “an illustration of the kind of plot outlines we would like to generate” (Lebowitz 1985, 172). Unfortunately, Universe was never able to display the level of mastery achieved by the authors of Days of Our Lives—a remarkably popular and long-running daytime television melodrama. This story, however, does nonetheless point to a number of crucial ways in which the goals of Universe are significantly different from those of systems such as Tale-Spin and Minstrel.

First, Universe is designed to generate continuing serials: stories that never end. Second, Universe is working in one of the world’s most popular story forms (television melodrama) rather than the somewhat archaic (and more difficult for contemporary audiences to judge) forms of Aesop-style fables and tales of Arthur’s knights. Third, Universe’s goals are defined in terms of what kinds of story and character structures it will generate, rather than in terms of the model of human cognition that the system’s operations will simulate.

The last of these, I believe, the most critical. While ideas such as scruffy AI’s “memory organization points” are important in the conception of Universe, the system is not presented as a simulation of a model of human cognition.6 Instead, it is presented as means of generating a universe of characters and an ongoing plot that interconnects them. In fact, in lieu of any cognitive science theory, Lebowitz writes: “Our methods are based on analysis of a television

