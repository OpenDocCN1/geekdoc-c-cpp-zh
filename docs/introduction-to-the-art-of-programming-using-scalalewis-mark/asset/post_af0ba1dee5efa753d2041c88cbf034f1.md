
used an octree, but many newer implementations use a kD-tree. The idea of a gravity tree code is that while the gravity from nearby masses needs to be handled exactly, the precise locations of individual bodies is not significant for things that are far away. For example, when calculating the gravity due to the Jupiter system on a mass, if the mass is near Earth, you do not need to do separate calculations for all the moons. Doing a single calculation for the total mass of the system at the center of mass of the system will be fine. However, if you are at the location of one of the outer satellites of Jupiter, the exact positions of some of the moons could be significant.

To quickly approximate the force of gravity from distant collections of mass, the tree can be augmented with information about all the particles in a subtree. The simplest augmentation is that each node stores the total mass and center of mass location of that subtree. To calculate the gravity force on a particle, the code does a recursive descent of the tree. At any given node, a check is done comparing the size of the node to its distance from the particle currently under consideration. If the condition $d < \beta s$, where $d$ is the distance between particle and node, $s$ is the size of the node, and $\beta$ is a parameter to adjust accuracy, ${}^{4}$ then the recursion must go down to the children. If that condition is not met, the force can be calculated against the center of mass of that node and the children can be ignored.

> ${}^{4}$For a monopole tree as described here, the value of $\beta$ should be between 0.1 and 0.3. Smaller values made the calculations more accurate, but increase the amount of work that is done.

## Chapter 36
## Wrapping Up

- 36.1 What You Have Learned ......................................................... 865
- 36.2 The Possibilities/A Pet Project .................................................... 866
- 36.2.1 General 2-D Application ....................................................... 866
- 36.2.2 3-D Application ............................................................... 866
- 36.2.3 Mobile ................................................................... 867
- 36.2.4 Web ..................................................................... 867
- 36.2.5 GPGPU ................................................................... 867
- 36.2.6 AI, NLP, and Machine Learning ................................................... 867
- 36.2.7 Open-Source and More ....................................................... 868
- 36.3 End of Chapter Material ....................................................... 868
- 36.3.1 Exercises ............................................................... 868
- 36.3.2 Projects ............................................................... 868

We have reached the end of our tour of programming. While this book has covered a good number of different topics, this is only a basic introduction to programming, which is but a stepping-stone into the field of Computer Science. The goal of this book was to lay a foundation that you can build on going forward. Now it is your job to continue the construction process.

### 36.1 What You Have Learned

The early parts of this book focused primarily on basic constructs used to tell a computer how to do things. You learned the use of conditional logic and looping constructs that could be put around simple sequential commands to express actions that you wanted to have the machine carry out. You learned how to break problems into pieces. At first the approach was to build separate functions that handled one part of the problem at a time, and ways of grouping data that made sense. Later on you saw that problems can be decomposed into objects that combine data with functionality. This learning to break problems apart should have had an impact on how you looked at many things through your life and in your studies outside of Computer Science.

A further step in how you approached problems came in the form of thinking about abstractions. It was possible to write a solution to one problem, but so much more could be gained if you tune that solution so that parts of it can be made to work in many different problems. The desire to abstract code appeared in many different contexts through the book with abstractions that varied over types, functionality, or both.

The modern world is teeming with data. Data is produced by all types of devices during all types of activities. You have learned how to give instructions to a computer to make it process data for you. There are limits on how much you can do by hand, but a computer can read and process millions or even billions of values quickly. You now know how to pull this data from files or over networks. You can deal with data in flat text, XML, or binary. You can use higher-order constructs to do the processing and apply multithreading to speed it up.

You also have the ability to write programs that display Graphical User Interfaces (GUIs) and draw custom graphics. You can write programs that talk to one another over networked sockets. When it really comes down to it, you have learned the basic tools to make a computer do pretty much anything. You have the foundation to create any application you can dream up.

### 36.2 The Possibilities/A Pet Project

So where should you go from here? Remember that programming is an art. You gain skill primarily by applying that art. If you do not apply it, you will lose your skill. As such, you need to exercise this art. There are many ways you can do this. The most important thing for you to do though is to pick a project. It does not have to be a really big project. If it is small, when you complete it you will simply pick another one. However, having a project outside of your normal course work gives you a great way to further develop your skills. It also allows you to build a portfolio of your work.

When you pick a project, you will need to look into what it takes to do it. Not all projects will favor you working in Scala. That is not a problem. Learning another language is a great exercise. It is always easier to learn the second than it was to learn the first and having knowledge of multiple languages often helps you to see problems from different perspectives. There are many types of projects that you can do in Scala though. Consider these possibilities.

#### 36.2.1 General 2-D Application

What you know how to do best at this point is write applications. If you can think of something that interests you that works as an application, run with it. Whether it is something useful or just something for fun, there are vast possibilities in what you can get a computer to do. Take advantage of your ability to do graphics and GUIs. Make something networked or push the parallelism to fully utilize newer hardware.

#### 36.2.2 3-D Application

If you are playing with graphics, you might want to do something in 3-D. You can render things in 3-D with ray tracing or other techniques that work in 2-D. However, if you are willing to do a bit of extra reading, which you should be, you can use Scala to write full 3-D applications through some different Java libraries.

The most standard 3-D graphics library is OpenGL®. There are several Java-based wrappers for OpenGL. The most established of these is called JOGL, the Java bindings for OpenGL. OpenGL takes advantage of 3-D hardware to make 3-D rendering fast.

The primary downfall of OpenGL is that it is a low-level API. That means you are setting up geometry and giving instructions to render it in a way that is close to what the machine wants. There are also higher level libraries like Java3D®. These use scene graph representations and can often be easier to use when you want to get things up and running.

New libraries are being written all the time. As of this writing, there are at least two different 3-D graphics libraries being developed specifically for Scala, including Sgine. More options will inevitably become available over time.

#### 36.2.3 Mobile

Not all applications have to run on desktop machines the way we have been working either. Mobile has become a huge market and you can do mobile development in Scala as well. The Android® platform from Google® uses Java for development by default, but it can work just as well with compiled Scala code as well. There is a project called “Scala for Android” that is being developed to help make it easier to put Scala programs on Android phones. This opens up phone and tablet options. The openness of the Android environment means that you can easily develop something to share with others.

#### 36.2.4 Web

Even on the desktop, many people do not use standard applications most of the time. Many of the things that you do on a computer have moved into the web browser. Rich web applications provide a very desktop-like feel with responsive user interactions, but they actually occur in the browser with information being stored out on the web.

You can use Scala for web development as well. Most of the large, well-known companies that use Scala at the time of this writing are in the web application field. The Lift® framework was the first web framework written specifically for Scala. By the time this book is published, version 2.0 of the Play! framework should also be available and should be part of the Typesafe stack. Version 2.0 of Play! has been written from the ground up for Scala and to take advantage of how Scala works. Typesafe support means that you can expect it to integrate nicely with other major pieces of the Scala tool set.

#### 36.2.5 GPGPU

In chapter 21 we looked at how you can use Scala to take advantage of multicore processors. New computers have more than just multicore processors though, they also have programmable graphics cards or processing units built into their CPUs that include graphics card style circuitry. In fact, a high-end gaming machine generally have more brute force computing power on the graphics card than in the normal processor. It is possible to write programs that take advantage of this processing power and do number crunching on graphics cards.

One standard for doing this type of work is OpenCL®. It is a library/language from the same group that created OpenGL. Just as JOGL is a Java binding for OpenGL, there is a Java binding for OpenCL called JavaCL that you can use to do low-level coding for Graphics Processing Units (GPUs) in Java and, therefore, in Scala as well. In addition, there is also a Scala addition currently under development called ScalaCL. Using ScalaCL, you can make collections that are similar to the parallel collections, but instead of using multiple threads on multicore machines, they take advantage of GPUs.

#### 36.2.6 AI, NLP, and Machine Learning

There are also libraries available that can get you up and running quickly on Artificial Intelligence (AI), Natural Language Processing (NLP), and machine learning. Remember that any library written for Java can be called easily in Scala as well. With just a little
