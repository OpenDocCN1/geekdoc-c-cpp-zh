
## Software Crisis

- Software is asked to perform demanding tasks these days:
  - Software controls critical space shuttle systems during launch
  - Software controls how the electricity generated in one power plant is added to that of the power grid that supplies a whole continent
  - Software controls elevators in hundred story office buildings
  - Software controls the routes taken by freighters across the oceans

- Software applications are complex because they model the complexity of the real world.

- The task of the software development team is to engineer the illusion of simplicity.

## Software Development Has Not Changed...

- New programs are created from scratch
- Difficult to reuse code
  - Goal of good programmers for years
  - Rarely achieve any reuse
- Procedural programming
  - Code and data defined separately
  - Data exposed to outside changes

## Software Crisis

### Manager's View
- Behind schedule
- Over budget
- Foreign competition

### Customer's View
- Buggy software lacks features
- Too expensive
- Why can't you make this "little" change?

### Programmer's View
- Multiple platforms
- Client/Server Applications
- GUIs

## What's the Big Deal?

| Category | Number of Programmers | Duration | Lines of Code |
| :--- | :--- | :--- | :--- |
| Trivial | 1 | 1-4 weeks | 500 |
| Small | 1 | 1-6 months | 1-2K |
| Medium | 2-5 | 1-2 years | 5-50K |
| Large | 5-20 | 2-3 years | 50-100K |
| Very Large | 100-1000 | 4-5 years | 1M |
| Extremely Large | 2000-5000 | 5-10 years | 1-10M |

## OOP is a New Approach...

The object-oriented approach is, in its simplest form, based on a seemingly elementary idea:

Computing systems perform certain actions on certain objects. To obtain flexible and reusable systems, it is better to base the structure of software on the objects rather than on the actions.

## OOP Questions

Once we have said this, we have not really provided a definition, but rather posed a set of problems:

- What precisely is an object?
- How do you find and describe the objects?
- How should programs manipulate objects?
- What are the possible relations between objects?
- How does one explore the commonalities that may exist between various kinds of objects?

How do these ideas relate to classical software engineering concerns such as:

- Correctness / Ease of use / Efficiency

## OOP Techniques

- Answers to these issues rely on an impressive array of techniques for efficiently producing reusable, extendable, and reliable software:
  - A new view of types and type checking
  - Information hiding (encapsulation)
  - Inheritance (linear & multiple)
  - Dynamic binding & polymorphism

Efficient implementation techniques have been developed to allow practical application of these ideas.

We study the object-oriented approach as a set of principles, methods, and tools which can be instrumental in building software of higher quality than is the norm today.

## OOP is a New Approach

- Programmer creates logical objects that combine data and functionality
- Programmer creates fully tested and debugged classes
- Reusing code decreases the amount that must be written for new applications

## Goal of OOP

- Reduce complexity in large system development
- Facilitate design and maintenance
- Reduce software development costs
- Provide reusable code

## Object-Oriented Programming

- OOP is programming by simulation

## Object-Oriented Programming

- OOP is most easily described as programming by simulation
- The programming metaphor is based on personifying the physical or conceptual objects from some real world domain into objects in the program domain.
- For example, objects are:
  - Clients in a business
  - Foods in a produce store
  - Parts in a factory
  - Chips on a circuit board

## Object-Oriented Programming

We try to incorporate objects from the problem domain into our computer models ...

... giving the objects in our program the same characteristics and capabilities as their real-world counterparts.

## Power of Simulation

- The power of simulation as a programming metaphor can be seen from the success of the window-based user interface now common in personal workstations.
- Apple Macintosh and Microsoft Windows, for example, use a desktop metaphor in which icons representing such common office objects as documents, clocks, folders, and trash cans can appear on the desk.

## Power of Simulation

- Interactively, a user can:
  - Open documents
  - Copy documents
  - Store documents with other documents in a folder
  - Place documents in a trash can

The key here is that operations on the desktop objects mimic the way their real-world counterparts are manipulated.

## OOP is Programming by Simulation

When implementation domain objects have a direct mapping to problem domain objects, the resulting software is far easier to understand and use.

## Traditional vs OOP

- OOP is fundamentally different from traditional procedural or algorithmic approaches.
- OOP describes a system in terms of the objects involved, whereas traditional programming approaches describe systems in terms of their functionality.

## Simple Video Game

We'll look at a video game example to illustrate the differences between traditional and object-oriented approaches.

Consider the following problem specification for a simple video game. A typical display for the game is shown in the next slide.

## Simple Video Game

![](img/7f36c52b5170b89b142dbb7b1ea4666b_556_0.png)

## Simple Video Game

- The objective of the game is to remove all the bricks from the wall.
- When a ball strikes a brick, the brick disappears.
- The ball can be redirected using the paddle that the player can move to the left or right using the mouse.
- The ball bounces off the sides, bricks, and paddle in a conventional manner.
- A player is provided at most 3 balls (one at a time) to remove the bricks.
- A ball is lost if it passes below the paddle (i.e., the player misses it).
- Demolishing the bricks with the allocated 3 balls is a win. Failure to do so is a loss.

## A Traditional Approach

- The classical top-down stepwise refinement approach to problem solving involves refining a problem solution into greater levels of detail based upon functional decomposition

## Video Game - Phase I

```
while someone wants to play
set initial game display
play a single game
```

- The design could now be refined further by taking some of the abstract functions in the current solution such as:

```
set initial game display
play a single game
```

and decomposing them in a similar fashion.

## Video Game - Phase II

```
set initial game display
  draw wall
  draw sides
  initialize paddles
```

```
play a single game
  set score to 0
  set balls left to 3
  while balls left > 0
    play a ball
    decrement balls left
```

- The next step might be to refine the play a ball module

## Video Game - Phase III

```
play a ball
    enter new ball into game
    while ball is in play
        check ball position
        update score and display
        move ball
        move paddle
remove ball from game
```

- We are refining the solution to the problem algorithmically in a step-by-step manner, with each step in the process describing a solution to the problem at a certain level of abstraction.
- Systems refined in this way are most easily described using a diagram where major modules are hierarchically organized and where each module represents a function or sub-problem in the solution.

## Functional Decomposition of the Video Game

- Video Game
- Set Initial Game Display
- Play a single game
- Draw Wall
- Draw Sides
- Initialize Paddle
- Play a Ball
- Check Ball Position
- Update Score and Display
- Move Ball
- Move Paddle
