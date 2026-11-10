
the AI in terms of strong code dependencies. As we have shown here, a statechart-based approach greatly helps in exposing the reuse opportunities, encapsulating the reuse at an appropriate level that encompasses not just a specific mechanic, but the high-level, behavioral abstraction. By composing functional groups of behaviors, novel AIs can then be directly constructed from a library of AI modules, a very practical strategy we demonstrate in the design of the Scythe AI development tool.

A primary benefit of formalizing reuse as we have done is in further being able to validate and perhaps even procedurally generate new AIs. Our design facilitates model checking and verification, and as part of future work, we are developing analyses that help in identifying and avoiding some of the more intricate logical errors that may arise in combining larger and more complex AI modules. Implicit state or message dependencies, for example, are a potential concern that may be addressed through deeper analysis of functional group behaviors, as well as through more formal means of specifying statechart interactions, such as found in protocol state machines.

Application of this reuse approach to more complex AIs is certainly possible. For example, NPCs in first-person shooter games employ tactical movement and cover, squad behaviors, and extensive combat behaviors such as ranged and melee weapons, vehicle-based combat, and fleeing. The *HALO* AI, taken from the successful *HALO* line of games, was reworked into the layered-statechart approach [19], and found to require 48 statecharts. This granularity affords considerable flexibility to the developer practicing reuse and provides an excellent start to any reuse library.

### REFERENCES

- 1. Brian Schwab, Dave Mark, Kevin Dill, Mike Lewis, and Richard Evans. GDC: Turing tantrums—AI developers rant. http://www.gdcvault.com/play/1014586/Turing-Tantrums-AI-Developers-Rant, 2011.
- 2. Christopher Dragert, Jörg Kienzle, and Clark Verbrugge. Toward high-level reuse of statechart-based AI in computer games. In *Proceedings of the 1st International Workshop on Games and Software Engineering*, pp. 25–28. Honolulu, HI, May 2011.
- 3. Jörg Kienzle, Alexandre Denault, and Hans Vangheluwe. Model-based design of computer-controlled game character behavior. In *MODELS*, vol. 4735, *LNCS*, pp. 650–665, 2007.
- 4. Unreal Technology. The Unreal Engine 3. http://www.unrealengine.com, 2007.
- 5. Curtis Onuczko, Maria Cutumisu, Duane Szafron, Jonathan Schaeffer, Matthew McNaughton, Thomas Roy, Kevin Waugh, Mike Carbonaro, and Jeff Siegel. A pattern catalog for computer role playing games. In *GameOn North America*, pp. 33–38. Eurosis, August 2005.
- 6. Brent Laming, Joel McGinnis, and Alex Champandard. Creating your building blocks: Modular component AI systems. http://www.gdcvault.com/play/1014573/Creating-Your-Building-Blocks-Modular, 2011.
- 7. Max Dyckhoff. Evolving Halo’s behaviour tree AI. Presentation at GDC. http://halo.bungie.net/inside/publications.aspx#pub15065, 2007.
- 8. John Walker, Robert Zubek, and Phil Carlisle. Little big AI: Rich behavior on a small budget. http://www.gdcvault.com/play/1012483/Little-Big-AI-Rich-Behavior, 2010.
- 9. Daniel Fu and Ryan T. Houlette. Putting AI in entertainment: An AI authoring tool for simulation and games. *IEEE Intelligent Systems*, 17(4):81–84, 2002.
- 10. Sunbir Gill. Visual Finite State Machine AI Systems. http://www.gamasutra.com/features/20041118/gill-01.shtml, November 2004.
- 11. David Harel and Hillel Kugler. The Rhapsody semantics of Statecharts (or, on the executable core of the UML). *LNCS*, 3147:325–354, 2004.
- 12. John Krajewski. Creating all humans: A data-driven AI framework for open game worlds. http://www.gamasutra.com/view/feature/1862/creating_all_humans_a_datadriven_.php, 2009.
- 13. Damian Isla. Handling complexity in the Halo 2 AI. *Game Developers Conference*, p. 12. San Francisco, CA, March 2005.
- 14. Chong-U Lim, Robin Baumgarten, and Simon Colton. Evolving behaviour trees for the commercial game DEFCON. In *Applications of Evolutionary Computation*, vol. 6024, *LNCS*, pp. 100–110. Springer, 2010.
- 15. Jeff Orkin. Three states and a plan: The AI of F.E.A.R. In *Proceedings of the Game Developer’s Conference*. http://alumni.media.mit.edu/~jorkin/gdc2006_orkin_jeff_fear.pdf, 2006.
- 16. Rodney Brooks. A robust layered control system for a mobile robot. *IEEE Journal of Robotics and Automation*, 2(1):14–23, 1986.
- 17. Philipp Kohloff. Level up for finite state machines: An interpreter for statecharts. In Steve Rabin (ed.), *AI Game Programming Wisdom 4*, pp. 317–332. Charles River Media, Hingham, MA, 2008.
- 18. Christopher Daggett, Jörg Kienzle, and Clark Verbrugge. Reusable components for artificial intelligence in computer games. In *Proceedings of the 2nd International Workshop on Games and Software Engineering*, pp. 35–41. Zurich, Switzerland, June 2012.
- 19. Christopher Daggett, Jörg Kienzle, and Clark Verbrugge. Statechart-based AI in practice. In *Proceedings of AIIDE*, Palo Alto, CA, October 2012.

## Repurposing Game Play Mechanics as a Technique for Designing Game-Based Virtual Worlds

Walt Scacchi

### CONTENTS

- 11.1 Overview 242
- 11.2 Related Research on the *What* and *How* of Repurposing Game Play Mechanics 242
- 11.3 Case Studies in Repurposing Game Play Mechanics 242
  - 11.3.1 Case 1—Producing Functionally Similar Games 244
  - 11.3.2 Case 2—Modding an Existing Game via New Game Play Levels, Characters, and Play Objectives 246
  - 11.3.3 Case 3—Replacing Multicharacter Dialogs and Adding Rashomon-Style Role-Play 248
  - 11.3.4 Case 4—Recognizing Resource Allocation Challenges with Uncertainty in Problem Domain 251
  - 11.3.5 Case 5—Choosing Meta-Problem Solving Domains for Game Development, Extension, and Play 254
- 11.4 Comparative Case Analysis: The Emerging Technique of Repurposing Game Play Mechanics for Game Design 256
- 11.5 Conclusions 257
- Acknowledgments 258
- References 258

### 11.1 OVERVIEW

This chapter examines the concept and practice of repurposing game play mechanics as a game design technique. Section 11.2 begins with a review of related research that informs this view of repurposing as a game design technique that may be adopted and practiced by new game developers or game players who want to engage in end-user game software development. Next, the chapter describes five game design case studies where different forms of repurposing are employed. These case studies include the identification of the example games and play mechanics that served to inform the resulting game designs from each. Each case study also categorizes the kinds of repurposing methods that were employed in reusing and adapting the source game mechanics into those employed in the new game design. Finally, the chapter includes a simple comparative analysis and a summary of these repurposing methods, as a basis for generalizing the method as a reusable and adaptive game design technique.

### 11.2 RELATED RESEARCH ON THE WHAT AND HOW OF REPURPOSING GAME PLAY MECHANICS

Designing computer games or game-based virtual worlds is a challenging problem (Bartle 2004). Such a problem has the complexity of both software systems design and designing the fun interactive play experiences (Fullerton et al. 2004; Howard 2008; Schell 2008). For the software engineering specialist new to game development, a clean-sheet game design can be a daunting challenge. Therefore, developers are wise to first start by examining the existing games and game play experiences as a basis for designing future games. Such an approach relies on some form of informal domain analysis (Prieto-Diaz and Arango 1991) to identify recognizable game features and capabilities, and game objects; functional operations; game play rules; and relationships between objects, operations, rules, features, and capabilities, as game play mechanics (Sicart 2008).

A formal domain analysis might have the potential to give rise to a persistent set of reusable game components, play mechanics, and eventually a meta-design theory for games (cf. Koehne et al. 2011) that could enable the
