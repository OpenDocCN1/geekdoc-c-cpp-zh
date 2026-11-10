# Chapter 1

# Getting Started

+   - 1.1 Languages and Libraries — 1
+   - 1.2 Installation and Configuration — 4

![](bbox=[0.441, 0.297, 0.583, 0.316])

Graphics programming has a reputation for being among the most challenging computer science topics to learn. These days, graphics programming is shader based—that is, some of the program is written in a standard language such as Java or C++ for running on the CPU and some is written in a special-purpose shader language for running directly on the graphics card (GPU). Shader programming has a steep learning curve, so that even drawing something simple requires a convoluted set of steps to pass graphics data down a “pipeline.” Modern graphics cards are able to process this data in parallel, and so the graphics programmer must understand the parallel architecture of the GPU, even when drawing simple shapes.

The payoff, however, is extraordinary power. The blossoming of stunning virtual reality in videogames and increasingly realistic effects in Hollywood movies can be greatly attributed to advances in shader programming. If reading this book is your entrée into 3D graphics, you are taking on a personal challenge that will reward you not only with pretty pictures but with a level of control over your machine that you never imagined was possible. Welcome to the exciting world of computer graphics programming!

# 1.1 Languages and Libraries

Modern graphics programming is done using a graphics library. That is, the programmer writes code which invokes functions in a predefined library (or set of libraries) that provide support for lower-level graphical operations. There are many graphics libraries in use today, but the most common library for platform-independent graphics programming is called OpenGL (Open Graphics Library). This book describes how to use OpenGL for 3D graphics programming in Java.