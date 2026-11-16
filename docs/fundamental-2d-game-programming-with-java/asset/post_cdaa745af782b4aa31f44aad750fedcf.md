

| Chapter/Section | Page |
|-----------------|------|
| Chapter 18 Conclusion | 609 |
| Chapter 1 -- "Hello World" | 610 |
| Chapter 2 -- "Input" | 610 |
| Chapter 3 -- "Transformations" | 610 |
| Chapter 4 -- "Time and Space" | 611 |
| Chapter 5 -- "Simple Game Framework" | 611 |
| Chapter 6 -- "Vector2f Updates" | 611 |
| Chapter 7 -- "Intersection Testing" | 612 |
| Chapter 8 -- "Game Prototype" | 612 |
| Chapter 9 -- "Files and Resources" | 612 |
| Chapter 10 -- "Images" | 613 |
| Chapter 11 -- "Text" | 613 |
| Chapter 12 -- "Threads" | 614 |
| Chapter 13 -- "Sound" | 614 |
| Chapter 14 -- "Deployment with ANT" | 615 |
| Chapter 15 -- "Collision Detection" | 615 |
| Chapter 16 -- "Tools" | 615 |
| Chapter 17 -- "Space Rocks" | 616 |
| Resources and Further Reading | 617 |
| Index | 619 |

## INTRODUCTION

![](img/588a4cda8f2acae94a7e1987bf99400d_12_0.png)

Years ago, when I started my first professional job as a software developer, I was asked to code an applet. At the time, I didn't know a lot about the Java language. Throughout school I used C++ extensively, and while I had done some coding in Java, I viewed it as a slow and dumbed-down version of C++.

At the same time, I was buying and reading as many game programming books as I could get my hands on. One book on artificial intelligence that I was working through had great examples, but they were all C++ and DirectX. Since I was busy learning Java at work, I thought porting the examples to Java would be a good way to learn the language. After all, how hard could Java game programming be?

As I soon discovered, there was very little information available about making games in Java. What I did find centered on applet programming, with virtually nothing on making application-type games. After porting the examples to Java and discovering that it was possible and not difficult, I searched for the tutorial that explained it all. I never did find it, so I wrote my own.

After publishing two tutorials on gamedev.net and writing a software renderer from scratch in Java, I realized that the language had a lot to offer the game community. While working on the next series of tutorials, I ended up with so much information that a book seemed like a much better solution.

That is what you are now reading: one developer's toolkit of code and explanations to help speed up the process of game programming in Java. Hopefully, the following pages can answer all the necessary questions and help you get to the important stuff: making games.

## THE BOOK'S ORGANIZATION

This book is split into three sections. The first part, "The Foundations," covers all the concepts you need to create a simple prototype game. The next part, "The Polish," covers the other concepts needed to program a complete game. The last part, "The Complete Game," takes all of the concepts presented and creates a complete game from start to finish. The summary of the content is as follows:

### Part I: The Foundations

### Chapter 1: Hello World
This chapter creates a frame-rate class, using it to monitor application speed. Then windowed and full-screen game loops are demonstrated.

### Chapter 2: Input
This chapter creates classes for monitoring keyboard input, as well as absolute and relative mouse input. Example code demonstrates input handling inside a game loop.

### Chapter 3: Transformations
This chapter covers vectors, points, and matrix math, as well as translation, rotation, scaling, and shearing of points and vectors. Matrix transformations, as well as manual methods, are discussed, along with an introduction to Swing's transformation objects.

### Chapter 4: Time and Space
This chapter adds a game clock to the loop, allowing for frame-rate-independent object manipulation. Screen mapping is also explored, allowing any screen-space objects to be mapped from normalized device coordinates.

### Chapter 5: Simple Game Framework
This chapter uses all the previous code presented to create a simple game framework for use in the remaining examples.

### Chapter 6: Vector2f Updates
This chapter updates the Vector2f class, first introduced in Chapter 3, with all the necessary linear algebra needed for intersection testing.

### Chapter 7: Intersection Testing
This chapter covers the math and algorithms necessary to determine whether objects are overlapping or inside each other. Points, circles, lines, and rectangles are used to explore this topic.

### Chapter 8: Game Prototype
This chapter uses the code presented so far, along with the simple framework, to create a prototype game. Although it's not yet a complete game, it presents a good idea of all the necessary code needed to make a game.

### Chapter 10: Images
This chapter covers working with images, creating images from scratch, and working with image files. It also covers using transparency, as well as different methods for drawing, rotating, and scaling images.

### Chapter 11: Text
This chapter covers everything you need to draw text using Java's Font library. There are also updates to the input library to support typing.

### Chapter 12: Threads
This chapter covers multi-threaded libraries available in Java, and demonstrates creating a non-blocking class, wrapping a non-blocking class with a blocking class, integrating multi-threaded code into a single-threaded game loop, and using a thread pool to speed up resource loading.

### Chapter 13: Sound
This chapter covers the problems with the sound support in Java. Both small clip files and large file streaming are explored, as well as using sound controls, such as pan and gain. The sound wrapper library developed in this chapter is used to integrate sound into the game loop with concepts explained in Chapter 12.

### Chapter 14: Deployment with ANT
This chapter presents an overview of the ANT build tool, and walks you through the process of creating an extendable build script for game development.

### Chapter 15: Collision Detection
This chapter covers determining the intersection point of colliding objects, as well as handling the collision response. Points, lines, rectangles, and circles are explored with many examples to study.

### Part III: The Complete Game

### Chapter 16: Tools
This chapter develops the tools necessary to make a complete game. Frameworks are developed for windowed games, full-screen games, and Swing editors. The utility library is updated, and a simple Swing editor is created to draw polygons and save them to XML. A sprite class is created, and a simple particle engine is explored.

### Chapter 17: Space Rocks
This chapter uses all the code presented to make a complete game from start to finish. Although this game is short and easy, it is complete, with a loading screen, attract mode, gameplay, high-score input and saving, and a deployment ANT script. Hopefully, seeing the work needed to create a complete game will motivate you to finish your own.

### Chapter 18: Conclusion
This chapter wraps up the entire book by listing all the code examples. This section presents a list of code examples by chapter, and each example explains the lessons learned, so finding an example is easy.

## WHO SHOULD READ THIS BOOK?

This is written for anyone who wants to learn the fundamentals of 2D game programming. While current graphics are evolving very fast, 3D graphics are only a piece of the puzzle. If a programmer does not understand the game loop, input handling, matrix math, intersection testing, collision detection, image rendering, threads, sound, or deployment, 3D graphics are not going to make the game playable. Even though 3D rendering is exciting, learning the fundamentals is important for having a solid foundation and the tools necessary to tackle any situation.

Although this book assumes the reader understands core programming concepts, object oriented software, and the Java programming language, no assumptions are made about previous game programming knowledge.

You should already be familiar with the Java language, as this is not covered in the text.

## SOFTWARE AND VERSIONS

This code has been tested on Windows 7 with the latest Java SE 6.0 and Java SE 7.0 versions available at the time of this writing. The Eclipse Helios IDE was used for compiling and execution of the code. The 1.8.2 ANT version was used for deployment.

The source code examples, as well as sound, image, and resource files, are available from:

http://www.indiegameprogramming.com

You can also download them from the book's website, where you can search for the book by title or ISBN:

http://www.cengageptr.com/downloads

## CONVENTIONS USED IN THIS BOOK

Monospace font is used for the following:

- Java classes
- Java methods
- Variable names
- Math variables and constants
- Code examples
- Code snippets
- XML
- Command-line output

