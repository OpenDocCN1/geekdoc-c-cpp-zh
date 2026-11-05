customer sign it, and the bottom line is that if you provide a system which behaves according to the design specification the customer must pay you. Once you have got your design specification you can think about ways of solving the problem. You might think that this is not necessary if you are writing a program for yourself; there is no customer to satisfy. This is not true. Writing some form of specification forces you to think about your problem at a very detailed level. It also forces you to think about what your system is not going to do and sets the expectations of the customer right at the start.

# Programmer's Point: The specification must always be there

> I have written many programs for money. I would never write a program without getting a solid specification first. This is true even (or perhaps especially) if I do a job for a friend.

Modern development techniques put the customer right at the heart of the development, and involve them in the design process. These work on the basis that it is very hard (and actually not that useful) to get a definitive specification at the start of a project. You as a developer don't really know much about the customer's business and they don't know the limitations and possibilities of the technology. With this in mind it is a good idea to make a series of versions of the solution and discuss each with the customer before moving on to the next one. This is called prototyping.

# 1.2.2 A Simple Problem

Consider the scenario: you are sitting in your favourite chair in the pub contemplating the universe when you are interrupted in your reverie by a friend of yours who sells double glazing for a living. He knows you are a programmer of sorts and would like your help in solving a problem which he has:

He has just started making his own window units and is looking for a program which will do the costing of the materials for him. He wants to just enter the dimensions of the window and then get a print out of the cost to make the window, in terms of the amount of wood and glass required.

"This looks like a nice little earner" you think, and once you have agreed to a price you start work. The first thing you need to do is find out exactly what the customer wants you to do...

# Specifying the Problem

When considering how to write the specification of a system there are three important things:

+   - What information flows into the system.
+   - What flows out of the system.
+   - What the system does with the information.

There are lots of ways of representing this information in the form of diagrams, for now we will stick with written text when specifying each of the stages:

# Information going in

In the case of our immortal double glazing problem we can describe the information as:

+   - The width of a window.
+   - The height of the window.

# Information coming out

The information that our customer wants to see is:

+   - the area of glass required for the window
+   - the length of wood required to build a frame.