
- Chapter 1, “Game Programming Overview,” looks at the fundamental concepts of game programming and how to get an initial game up and running. It also introduces the Simple DirectMedia Layer (SDL) library.

- Chapter 2, “Game Objects and 2D Graphics,” discusses how programmers organize the objects in their games and explores additional 2D graphics concepts, such as flipbook animation.

- Chapter 3, “Vectors and Basic Physics,” covers mathematical vectors, which are critical tools for any game programmer. It also explores the basics of physics, for use with both motion and collisions.

- Chapter 4, “Artificial Intelligence,” looks at approaches to make game characters that are computer controlled, including concepts such as state machines and pathfinding.

- Chapter 5, “OpenGL,” explores how to create an OpenGL renderer, including implementing vertex and pixel shaders. It includes a discussion of matrices.

![](img/e9afcec1487716b0ef80d7e7c09869c8_53_0.png)

Figure P.1 Chapter dependencies

- Chapter 6, “3D Graphics,” focuses on converting the code created so far to work for a 3D game, including how to represent the view, projection, and rotations.

- Chapter 7, “Audio,” covers how to bootstrap an audio system using the excellent FMOD API. It includes coverage of 3D positional audio.

- Chapter 8, “Input Systems,” discusses how to design a more robust input system for processing keyboard, mouse, and game controller events.

- Chapter 9, “Cameras,” shows how to implement several different 3D cameras, including a first-person camera, a follow camera, and an orbit camera.

- Chapter 10, “Collision Detection,” dives into methods of collision detection for games, including spheres, planes, line segments, and boxes.

- Chapter 11, “User Interfaces,” looks at implementing both a menu system and heads-up display (HUD) elements such as a radar and aiming reticule.

- Chapter 12, “Skeletal Animation,” covers how to animate characters in 3D.

- Chapter 13, “Intermediate Graphics,” explores a handful of intermediate graphics topics, including how to implement deferred shading.

- Chapter 14, “Level Files and Binary Data,” discusses how to load and save level files, as well as how to write binary file formats.

- Appendix A, “Intermediate C++ Review,” reviews several intermediate C++ topics used throughout the book including memory allocation and collections.

Each chapter includes a corresponding game project (with source code available, as mentioned), recommended additional readings, and a couple of exercises. These exercises generally instruct you to add additional features to the code implemented in the chapter.

## CONVENTIONS USED IN THIS BOOK

New terms appear in **bold**. Code appears in a monospaced font. Small snippets of code sometimes appear as standalone paragraphs:

```
DoSomething();
```

Longer code segments appear in code listings, as in Listing P.1.

## Listing P.1 Sample Code Listing

```
void DoSomething()
{
    // Do the thing
    ThisDoesSomething();
}
```

From time to time, some paragraphs appear as notes, tips, sidebars, and warnings. Here is an example of each.

> > note
> Notes contain some useful information about implementation changes or other features that are worth noting.

> > tip
> Tips provide hints on how to add certain additional features to your code.

> > warning
> Warnings call out specific pitfalls that warrant caution.

> > SIDEBAR
> Sidebars are lengthier discussions that are tangential to the main content of the chapter. This content is interesting but isn't crucial to understanding the core topics of the chapter.

## ACKNOWLEDGMENTS

Although this is not my first book, writing this one has been an especially long process. I am thankful that Laura Lewin, the executive editor on this book, was especially patient throughout the two years this book was in progress. I would also like to thank the rest of the team at Pearson, including Michael Thurston, the development editor on this book.

I would also like to acknowledge the work put in by the technical editors on this book: Josh Glazer, Brian Overland, and Matt Whiting. The technical reviews were critical in making sure both that the content was correct and that it was accessible for the target audience.

I'd also like to thank all my colleagues at the USC Information Technology Program and especially those who helped shape the curriculum of the games courses I teach: Josh Glazer, Jason Gregory, Clark Kromenaker, Mike Sheehan, and Matt Whiting. Much of the inspiration for this book comes from that curriculum. I would also like to thank all my excellent TAs over the years, who are too numerous to name personally.

I would also like to thank the content creators on sites like https://opengameart.org and https://freesound.org for creating excellent game content released under Creative Commons licenses. These sites were critical to finding assets for the game projects in this book.

Finally, I'd like to thank my parents, as well my sister, Nita, and her family. Without their support, inspiration, and guidance, I never would have gotten here in the first place. I'd also like to thank my friends, like Kevin, who understood when I couldn't go see the latest movie, go to dinner, or really do anything social because I was “working on my book.” Well, I guess I have time now....

## ABOUT THE AUTHOR

**Sanjay Madhav** is a senior lecturer at the University of Southern California, where he teaches several programming and video game programming courses. He has taught at USC since 2008.

Prior to joining USC, Sanjay worked as a programmer for several video game developers, including Electronic Arts, Neversoft, and Pandemic Studios. His credited games include *Medal of Honor: Pacific Assault*, *Tony Hawk's Project 8*, *Lord of the Rings: Conquest*, and *The Saboteur*.

Sanjay is also the author of *Game Programming Algorithms and Techniques* and co-author of *Multiplayer Game Programming*. He has a B.S. and an M.S. in computer science and is pursuing a Ph.D. in computer science, all from USC.

## CHAPTER 1

## GAME PROGRAMMING OVERVIEW

This chapter first discusses how to set up a development environment and access the source code for this book. Next, it covers the core concepts behind any real-time game: the game loop, how a game updates over time, and the basics of game input and output. Throughout the chapter, you will see how to implement code for a version of the classic game Pong.

### SETTING UP A DEVELOPMENT ENVIRONMENT

Although it's possible to write the source code for any program with a text editor, professional developers typically use an **integrated development environment (IDE)**. The advantage of an IDE is that it provides code completion and debugging in addition to text editing capabilities. The code for this book works on both Microsoft Windows and Apple macOS, and the choice of IDE depends on the choice of platform. For Windows, this book uses Microsoft Visual Studio, and for macOS, it uses Apple Xcode. The remainder of this section contains brief instructions on setup of these environments on their respective platforms.

### Microsoft Windows

For Windows development, the most popular IDE by far is Microsoft Visual Studio. Visual Studio also tends to be the most popular IDE for C++ game developers, with most PC and console developers gravitating toward the IDE.

This book uses Microsoft Visual Studio Community 2017, which is available as a free download at https://www.visualstudio.com/downloads/. Installation of Visual Studio Community 2017 requires Microsoft Windows 7 or higher.

When you run the installer program for Visual Studio, it asks which “workloads” it should install. Make sure to minimally select the Game Development with C++ workload. Feel free to also select any other workloads or options desired.

> warning
> THERE ARE DIFFERENT VERSIONS OF VISUAL STUDIO: There are several other products in the Microsoft Visual Studio suite, including Visual Studio Code and Visual Studio for Mac. Neither of these products are the same thing as Visual Studio Community 2017, so be careful to install the correct version!

### Apple macOS

On macOS, Apple provides the free Xcode IDE for development of programs for macOS, iOS, and other related platforms. The code for this book works in both Xcode 8 and 9. Note that Xcode 8 requires macOS 10.11 El Capitan or higher, while Xcode 9 requires macOS 10.12 Sierra or higher.

To install Xcode, simply go to the Apple App Store and search for Xcode. The first time Xcode runs, it asks if you want to enable debugging features. Make sure to select Yes.

### GETTING THIS BOOK'S SOURCE CODE

Most professional developers utilize source
