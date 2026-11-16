
## HOW IT WORKS

If you've read this far, you already know that you're not going to be able to just sit back and listen to me talk at you. At the core of this book are the exercises, and if you're going to learn, you'll need to work through them. Really do them. You can't just think about the answers. You need to sit down at the computer or pick up your pencil and do the work. Here's a taste of some of the things you'll be doing:

## THE THINKING HAT

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_15_0.png)

Most of the exercises in the book tell you to Put on Your Thinking Hat. I'll give you answers to these exercises, but it's really important to understand that you won't always get the answers completely right, and **that's okay**. It doesn't mean you're not “getting it”. It means that I don't always play fair, because you learn as much (or more) from your mistakes.

## ON YOUR OWN

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_15_1.png)

Some exercises ask you to do things on your own, and I won't give you the answers. Sometimes there really aren't answers; they're just things you need to think about. It might be tempting to put these aside for “later”, but it's best if you don't. They're part of the learning process.

## TAKE A BREAK

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_15_2.png)

From time to time I'll suggest that you take a break before you move on to the next section. Of course you can take breaks whenever you like, but these suggestions aren't because I think you might be getting tired. I make these suggestions because learning research tells us that if you stop for 15 minutes or so before you review, you're much more likely to transfer information to long-term memory. (In other words, you'll actually learn it.)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_16_0.png)

## APPLICATION DEVELOPMENT

So, you want to learn to program. That’s great. You’re reading the right book. But what exactly is programming? Is it the same as software development?

And what about that other stuff you might have heard about...development platforms, application architectures, development methodologies, design patterns, best practices. It all starts to sound a little scary, doesn’t it?

In this chapter, we’ll figure out what all these things are, and where they all fit in the process of getting from here (an idea for some software) to there (a working application).

Relax, it’s not as complicated as you think...

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_17_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_18_0.png)

A project begins when someone has an IDEA.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_18_1.png)

The idea gets translated into a specification.

- The SPECIFICATION tells the programmer what the system needs to do.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_18_2.png)

The software executes in a specific RUNTIME ENVIRONMENT, like Windows or a browser.

When people use your software, they'll often come up with new ideas...and the project starts all over again

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_19_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_19_1.png)

Using the specification, a programmer creates SOURCE CODE in a programming language like C#.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_19_2.png)

THE DEVELOPMENT ENVIRONMENT provides the tool to turn the source code into working software.

## Microsoft Visual Studio

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_20_0.png)

## HOW'D YOU DO?

I gave you a messy stack of paper and spool of wire. Thinking cap exercises don't always have a single right answer, but here are two things you might have done...

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_20_1.png)

You might have bound the papers into a notebook. That's a good permanent solution, but a lot of work.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_20_2.png)

Or you might have simply made a paperclip. Easy and fast, but probably temporary.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_20_3.png)

So what's the point here? That in application development the right answer is almost always “it depends”. The best solution will depend on how the application is going to be used. It will depend on how much time and effort are available (or you're willing to invest). It will depend on what else is going on in the application.

## The best solution depends on...well, it depends.

## LET'S REVIEW THAT PROCESS...

Start with a good idea (that's the hard part), and you're just five steps away from a solution. In this book we'll mostly be looking at how you write source code, but don't worry, we'll look at the rest of the steps too—at least enough to get you started on the right path.

- 0 Start with a good idea...
- 1 ...and then create a specification.
- 2 Use best practices...
- 3 ...to create the source code.
- 4 Create an executable...
- 5 ...to run in your chosen environment.

What's this stuff? These images represent system architectures, development methodologies, and best practices. These are the principles that make the difference between code that just works (mostly) and a reliable, maintainable application. They'll save you money and headaches down the road, and we'll talk about them in detail in this chapter and throughout the book...

## MEET NEIL & GORDON...

Before we get started, I'd like you to meet the clients we'll be working with. They run the hottest new cafe in town. But they're drowning in their own success. There's so much to manage! Schedules, menus, meetings, and now that their business is growing, they need to get all those yummy recipes out of their heads and into a useable form. The boys are geniuses in the kitchen, but they don't know where to start with this management stuff.

We'll be helping them out throughout the book.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_22_0.png)

## TASK LIST

In the rest of this book we'll go into detail about step three of the development process, writing C# code, and writing it well. But there are three things we need to examine first:

## THE DEVELOPMENT PROCESS

Everything we do fits into the context of the process of a whole, so we need to understand that first.

## SYSTEM DESIGN

We know that the development process begins with an idea that gets translated into a specification that describes how the system is to work. We'll start, then, by looking at a few tools for capturing the system design.

## CREATING EXECUTABLES

The integrated development environment (IDE) provides the tools that translate source code into an executable, a piece of software that a user or another piece of software can execute. We'll be using Visual Studio to create executables, and before we can make decisions about how to structure an application, we need a little more detail about how that works in the context of the .NET Framework.

## ON YOUR OWN

Do you have some ideas about applications you'd like to write? Make a note of three or four of them. We'll come back to them again and again.

## THE DEVELOPMENT PROCESS

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_24_0.png)

The application development process begins when somebody needs a computer to do something. That “something” might be a change to an existing piece of software or a completely new system, but most applications are (or should be) developed in response to a need.

The “something” that the application is to do is captured in a SPECIFICATION. A specification can be as simple as a diagram scribbled on a napkin or many volumes of detailed description. It might be “complete” before any code gets written, or it might be developed over the course of the project.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_24_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_24_2.png)

You’ll use the specification to develop the application. In doing so, you’ll choose an effective DEVELOPMENT METHODOLOGY (the set of steps you’ll perform during development) and be guided by best PRACTICES (rules of thumb that experience has shown result in more efficient and maintainable code). You may also implement design PATTERNS, which are standard solutions to common programming problems.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_24_3.png)
