
## Introduction

## Overview

In the fields of computer graphics and computer game development, the word *gem* has been established as a term for describing a short article that focuses on a particular technique, a clever trick, or practical advice that a person working in these fields would find interesting and useful. The term *gem* was first used in 1990 for the first volume of the *Graphics Gems* series of books, which concentrated on knowledge pertaining to computer graphics. The mainstream methods for rendering 3D images have changed considerably since then, but many of those gems still comprise useful techniques today and have demonstrated a timeless quality to the knowledge they contain. Several newer book series containing the word "Gems" in their titles have appeared in related subject areas such as game programming and GPU rendering, and they all advance the notion of sharing knowledge through concise articles that each focus on a specific topic. We continue the tradition with this book, the first volume of *Game Engine Gems*.

*Game Engine Gems* concentrates on knowledge relating to the development of game engines, which encompass the architecture, design, and coding methods constituting the technological foundation for today's video games. A complete game engine typically includes large components that handle graphics, audio, networking, and physics. There may also be large components that provide services for artificial intelligence (AI) and graphical user interfaces (GUIs), as well as a variety of smaller components that deal with resource management, input devices, mathematics, multithreading, and many additional pieces of generic functionality required by the games built upon them. Furthermore, many game engines are able to run on multiple platforms, which may include PCs and one or more game consoles such as the PlayStation 3 or Xbox 360. The *Game Engine Gems* series is specifically intended to include all such aspects of game engine development targeting all current game platforms.

This book is divided into three parts covering the broad subject areas of game engine design, rendering techniques, and programming methods. The 28 gems appearing in this book are written by a group of 25 authors having expertise in game engine development, some quite extensive. It is our hope that the wisdom recorded in these pages and the pages of future volumes of Game Engine Gems continue to serve game developers for many years to come.

## Call for Papers

At the time this book is published, work on the second volume of *Game Engine Gems* will have already entered its early stages. If you are a professional developer working in a field related to game development and would like to submit a contribution to the next book in the series, please visit our official website at http://www.gameenginegems.com/.

## Part I: Game Engine Design

### Chapter List

- Chapter 1: What to Look for When Evaluating Middleware for Integration
- Chapter 2: The Game Asset Pipeline
- Chapter 3: Volumetric Representation of Virtual Environments
- Chapter 4: High-Level Pathfinding
- Chapter 5: Environment Sound Culling
- Chapter 6: A GUI Framework and Presentation Layer
- Chapter 7: World's Best Palettizer
- Chapter 8: 3D Stereoscopic Rendering: An Overview of Implementation Issues
- Chapter 9: A Multithreaded 3D Renderer
- Chapter 10: Camera-Centric Engine Design for Multithreaded Rendering
- Chapter 11: A GPU-Managed Memory Pool
- Chapter 12: Precomputed 3D Velocity Field for Simulating Fluid Dynamics
- Chapter 13: Mesh Partitioning for Fun and Profit
- Chapter 14: Moments of Inertia for Common Shapes

### Chapter 1: What to Look for When Evaluating Middleware for Integration

Jason Hughes  
Steel Penny Games, Inc.

### 1.1 Middleware, How Do I Love Thee?

Modern games are very rarely works comprised entirely of proprietary, custom code written by in-house developers. The amount of polished functionality required to compete in the games industry is simply an enormous task for a single studio to undertake, and is in a word, unproductive. These days, game programmers are expected to be comfortable using certain wheels that have been invented elsewhere and only reinventing those that provide tangible benefits to their project or studio by directly contributing to the success of a title or differentiating them in some way from the competition. Given that some middleware libraries will be chosen to fulfill certain needs, and often there are several products to choose between with similar feature sets, we ask, "What are the considerations a team should take into account when comparing middleware products?"

Let's assume that the language of choice is C/C++, as is most common today with middleware and game development. Let's also assume that we're discussing an existing codebase where a specific feature is missing that can be filled by middleware, and that the team's desire is to be surgical during integration and leave the smallest scar possible should it need to be removed.

### 1.2 Integration Complexity and Modularity

The first, most important feature of a middleware package is its integration complexity. Good libraries are highly modular, minimally intrusive, and easy to plug into very different codebases. In short, they make very few assumptions and are fairly decoupled from implementation details of other systems. A good library should come with reasonable defaults or require very limited configuration before the system is in a testable, working state. The integration engineer's level of experience can play a role in the usability of a system, so minimal integration is key. This promotes a rapid evaluation cycle—it leaves a bitter aftertaste when an engineer has a long integration cycle, only to find the library is not desirable. My rule of thumb is two days. Anything that takes more than two days to get running will waste a week putting it through its paces, and there aren't enough weeks in a development cycle to try out alternatives.

### 1.3 Memory Management

Console developers all know that careful memory management is crucial to a stable product. Middleware intended for virtual memory-backed PC systems, or even those technologies with hefty demands that next generation consoles can satisfy, may not be suitable for the more modest RAM budgets of yesteryear. It's important to know not just what memory budgets are expected, but also who is responsible for managing the allocations.

Ideally, each middleware library will have its own memory management scheme that simply initializes with two arguments: a pointer to a block of memory and its size. A middleware library author is the person most knowledgeable of the sizes of allocations, the churn rate for allocations, and the memory management algorithm most appropriate to prevent fragmentation within their own allocation pool. Further, this has the advantage of explicitly notifying the developer when the memory budget has been exceeded, rather than collecting undesirable large amounts of memory from the main heap where tracking down memory consumption can be tedious and problematic. Also, this method tends to highlight integration mishaps where library assets are being leaked, because it soon fails when the heap is exhausted. A resizable heap is sometimes desirable, specifically if certain game levels need to shift memory privileges to emphasize different systems, though this feature is fairly rare.

In the absence of a completely isolated heap managed by the middleware library, a good fallback is one where you are expected to provide a pair of missing functions for `alloc()` and `free()`, you can override weakly declared functions with your own, or lastly, you can compile the library from source and are able to provide a `#define` macro used throughout for allocation. None of these methods incur per-allocation function call overhead because they are resolved by the compiler or linker. In this method, you have the option of forwarding allocations to the main heap
