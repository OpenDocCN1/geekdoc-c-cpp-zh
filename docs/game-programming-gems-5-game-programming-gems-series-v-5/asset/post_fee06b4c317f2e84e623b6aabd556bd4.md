
ized in shader programming and 3D graphics algorithms. Gábor's publications and programs can be found at http://www.geocities.com/gabsprog.

### Andy Thomason
athomason@acm.org

Andy Thomason has recently completed the game Galgeon with Toby Gard, designer of Lara Croft. Starting in the "70s with home-built 280 hardware, he has worked with Psygnosis and Rage and is currently a freelance technology researcher and boat builder in Bristol, England. He maintains a Web site at http://www.titboom.demon.co.uk/.

### Matthew Titelbaum
mtitelbaum@lith.com

Matthew Titelbaum is a senior software engineer at Monolith Productions, Inc., developing the AI systems for The Matrix Online MMORPG. After starting his career in the industry working on console titles at Crystal Dynamics, DreamWorks Interactive, and SCEA, he began his involvement with massively multiplayer games by joining Sony Online Entertainment. At SOE, he worked on Sovereign (an experimental MMO RTS title) and several EverQuest expansion packs; he is most proud of the contributions he made in overhauling and optimizing EverQuest's pathfinding system. Matthew has a B.S. in computer science from Carnegie Mellon University.

### Marco Tombesi
baggiol@libero.it

Marco Tombesi is an Italian computer engineer, graduated from the University La Sapienza of Rome in 2002 with a first class degree. He has been a freelance game developer for years and now is actually considered a C++ and OpenGL master. He has published a successful article in Game Programming Gems 2, "3ds max Skin Exporter and Animation Toolkit." Currently he is working on a soccer game project.

### Christopher Tremblay
chris@Barney.zapto.org

Christopher Tremblay lives in the San Francisco bay area. He holds a B.S. in software engineering and is nearing a B.S. in mathematics. His work in the industry covers varied subjects including game AI, core networking, software rendering algorithms, and 3D geometry algorithms down to low-level and optimization. He currently works for Motorola where he is building the next generation 2D/3D graphics rasterization engine for the next generation of cell phones. In his spare time, you may find him bruising himself with roller blades in the skate park, snowboarding, or yes, even with the radiation of his monitor while programming.

### Bretton Wade
brettonw@microsoft.com, Bretton_Wade@acm.org

Bretton Wade is a 10-year veteran of the games and graphics industries, currently working as a manager in the Xbox system software team and as an instructor in the highly praised University of Washington Extension Game Development course. Previous game development roles include title lead for an independent studio contracted by Blizzard Entertainment, development lead on Microsoft's Flight Simulator, and individual contributor roles in a variety of titles published by Microsoft Game Studios. Bretton worked on VR authoring tools at SGI, and was a research engineer for Advanced Rendering Technology and Microsoft Research. He is a graduate of Virginia Tech and holds a master's degree from the Cornell University Program of Computer Graphics.

### Niniane Wang
niniane@gmail.com

Niniane Wang worked for Microsoft Games for five years, most recently as a dev lead on Flight Simulator 2004. Her work on weather graphics has been presented in SIGGRAPH, GDC, GDMag, and academic publications. She holds a bachelor's in CS from Caltech and a master's in CS from the University of Washington. Currently, she is a software engineer at Google.

### Jon Watters
hplus-gpg5@mindcontrol.org

At 10 years of age, Jon started creating software and has never stopped. He helped deliver several large products, including the CodeWarrior development tools, the BeOS multimedia operating system, and the There virtual world. Jon currently works at Forterra Systems on a massively distributed simulation platform.

## SECTION 1

### GENERAL PROGRAMMING

### Introduction

### William E. Damon III
wdamon@ati.com

Content—the background art, settings, locations, characters, plots, stories, and actions that breathe life into the game experience—drives hit titles. For the production staff, this means constructing their product around a solid premise and employing outstanding, disciplined service organizations. The Information Technology department might spring to mind, but the organization addressed here is actually the software engineering team.

Software engineers solve problems. Sometimes problems in game programming are solved with a tremendous amount of programming effort, but a transition in thinking is occurring. Game programming is evolving into a disciplined practice of engineering general solutions for broader and more reusable application, whether it is adopting and adapting a middleware technology or creating something in-house. This evolution is allowing engineers more time to solve the real problems faced by their customers, the content creators, rather than reinventing old solutions. As a result, content creators are enabled to more rapidly iterate over implementations, tuning and tweaking details to achieve higher quality in the final product.

This is the common thread that runs through all the articles in this section. Whether discussing improved designs for low-level libraries built for other engineers on the project to use, general yet intelligent memory management techniques for the core of the systems (game, editor, or otherwise), remote debuggers, and/or visual and scriptable environments for designing user interfaces, all the articles in this section are aimed at providing reusable components in the production pipeline.

You'll see a broad range of topics in this section—and even various solutions for particularly large problems—to help guide you in building the best suite of tools for the title at hand. Absorb these articles, for as an engineer who solves problems, you never know when one will come in handy!

### Context-Sensitive HUDs for Editors

Adam Martin, Grex Games
gpg@grexengine.com

Most games need custom graphical tools for content creation (level layout, AI behavior editing, etc.). Really good tools can greatly increase the efficiency of the content development team, often multiplying the amount of content created by a large ratio. For instance, one good level-editing tool can easily make a single level-designer become as productive as three equivalent designers working with inferior tools. However, excellent tools often turn out to be inordinately expensive, making it difficult to justify the risks of initial development, or the continued costs associated with maintenance.

This gem provides an approach to _heads-up editing_ using some very simple techniques. It is designed to be extremely simple to maintain and should alleviate many of the costs and difficulties of in-house editor development. It unlocks end-user (designer) productivity boosts in earlier stages of the tool development process and reduces some of the project risks.

### Problems

There are four sets of problems that apply to custom editors, each of which we will cover in detail to explain how and why the idea behind this gem works.

The first set of problems is due to the inherent complexity of a custom content editor. Custom editors always become complex (some would say _bloated_) sooner or later; if their work was simple, mainstream editors would have been sufficient in the first place, and the cost of making a custom editor could have been avoided altogether.

The other sets of problems are each associated with a particular role in the development team. For example, the ways in which content authors use the editor create problems unique to those people.

### Editor and GUI Complexity

Taking a 3D modeler as an example, we usually have four views of the object being edited, each view represented in a dedicated viewport. Each viewport has to be

| Display | Controls |
| :--- | :--- |
| Show the position of the look_at point | Zooming in and out (i.e., altering FOV) |
| Show the positions of the different viewports cameras in the other viewports, where visible | Panning in two dimensions |
| Render the "document" (3D model) | Rotation about three axes |
| Render world-landmarks (primary Cartesian axes, positive/negative axis directions, etc.) | Translation in three dimensions |
| Render the precise Cartesian coordinates of each salient item, at least the camera and the look_at point | Select each and every option to act upon EITHER the camera OR the look_at point OR both of them |

So, for an "editor" that lets you do nothing more than move the cameras about (and without any fancy controls for doing so; just the basics!). We have five separate things that have to be displayed and five separate sets of controls to provide. These 10 items each requires unique algorithms, and although the algorithms themselves are simple to implement, they still need to be written. Already, we have enough separate algorithms (each of which we want to maintain, update, replace, and/or remove separately) that it would be nontrivial to maintain, and we haven't yet added essential features such as object selection and basic editing.

Typical game content editors consist of perhaps 50 unique display algorithms and 30 or more control algorithms, with continuous extension. This can be a nightmare to maintain, and most editors soon become so unwieldy (in terms of both code and architecture) that adding even the simplest of functionality incurs considerable cost. This is especially hard to justify when the end consumers (players) are often not even going to see the tool.

### Users

The end users of content-editing tools are rarely the programmers. Although programmers do develop and use editors (including IDEs, of course) such tools are usually developed to make it easy for nontechnical people to create or customize content for the game. On large projects, the primary users are usually artists (creating 2D and 3D graphical content), writers (creating quests, subplots, game-logic widgets, etc.), and interpreted/proprietary-language programmers (e.g., developing AI scripts).

The main requirements for this set of users are:

- A powerful, feature-rich graphical user interface (GUI)
- Extendible, with the ability to add new features over time (an iterative process of end users' feedback to the tools' developer(s) resulting in new functionality)
- Reliable; most editing should be quick and easy for the end user, and the tool(s) must be stable
