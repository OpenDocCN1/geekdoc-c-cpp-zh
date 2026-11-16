
ptrG = GetFirst<G>();

This code does not need to be altered if the hierarchy changes since the CEH manager does all the work of locating the first instance of class G and returning a pointer to it. This is how using CEHs can make your code more resilient to code restructuring. The introspection system can also provide APIs that deal with vectors of objects and filtering of objects based on relative location (above, below, etc.). Object linkage is no longer explicit in code, but dynamic at run time.

## Visualization

Visualizing the execution of your code can be a great help in debugging and bringing new members of your team up to speed with your code. Using a CEH can help make this visualization consistent and useful. Since the calling graph and actual call order are controlled by your manager class, you can get the manager to output data about your execution behavior for you. A handy format that I use is to output the execution graph in DOT file format [1], and then run this file through GraphViz to get a snapshot of how the code is linked and executed.

## Deferred Operations

There are certain operations that are very dangerous to perform while you are mid-way through the graph traversal. Any operation that modifies the graph (delete, move, create) during the update phase can have disastrous effects since you are altering the same tree you are traversing. To shield against this, dangerous operations can be queued until the end of the update phase. These deferred housekeeping tasks can catch you out if you are expecting the modifications to happen immediately, but the added layer of bug protection it gives you is worth the trouble.

## 23.3 Benefits & Pitfalls

Moving your execution control over to a data driven, dynamic system like code execution hierarchies has both benefits and pitfalls. The benefits include:

- Code is constructed with a consistent pattern (Init, Update, Destroy, etc.).
- Update order is easier to modify since the order is dynamic rather than hardcoded.
- Introspection can make finding object instances easier than manually navigating class linkages.
- Introspection allows the layout of objects to change without the need to maintain manual linkage code.
- It is simple to visualize the execution order and hierarchy of your code. This aids debugging and teaching of programmers new to the team.

There are, of course, a few pitfalls and caveats that come with the use of code execution hierarchies. These include:

- It is difficult to see what is happening by just looking at the code. Since the update order is dynamic and built at run time, manual inspection of the source code doesn't help much.
- Some code simply doesn't fit. Even though CEHs provide a simple and flexible structure, there are still pieces of functionality that don't fit into the framework. You still have to deal with these systems manually and take care of object linkage by hand.
- You need to be careful with your granularity. Putting game systems and substantial game objects into the CEH can be very useful. Placing every particle in a particle system is overkill, and you will waste lots of CPU cycles and memory to unnecessary CEH overhead. You need to use your judgement.
- Modifying the execution tree while you are traversing it can cause lots of catastrophic but difficult-to-find bugs. You need to be very careful when altering the tree or defer all modification operations until after the update phase has completed.

Code execution hierarchies are a huge topic for discussion. I have worked with code that uses explicit execution order, linear lists or queues of update functions, and deeply embedded tree hierarchies, and they all have their good and bad points. My hope is that this gem has introduced a new way of thinking about code execution to those who have not used dynamic systems before and has possibly provided some food for thought for those currently using dynamic execution systems. Game code inevitably becomes complex, and new ways of looking at how we construct code are always useful. Using consistent and flexible methods like those I have described can help ease the pain and provide much needed abstractions.

## References

- [1] DOT file format. http://www.graphviz.org/doc/info/lang.html
- [2] GraphViz. http://www.graphviz.org/

## Chapter 24: Key-Value Dictionary

Martin Linklater

Sony Studio Liverpool

### Overview

This gem presents a design for a flexible, observable repository for game configuration data. The key-value dictionary (KVD) is a data structure inspired by the key-value observing [1] technology used in Mac OS X Cocoa frameworks. When used sensibly, the KVD can simplify your code.

The KVD is designed to be flexible, easy to use, and have few external dependencies. It is not designed to be blisteringly fast, or to be used for frequently modified data. The KVD is well suited for storing game state information that is read often, but modified rarely. The KVD code on the accompanying CD is written in C++ and uses the standard template library (STL) for internal storage containers. The KVD is lightweight (about 350 lines of C++) and simple to integrate into an existing game engine.

### 24.1 Design

Apple's OS X relies heavily on Objective-C and the Cocoa frameworks. One of the fundamental mechanisms of Cocoa that binds the frameworks together is called "key-value observing" (KVO). Apple describes KVO as follows:

> Key-value observing provides a mechanism that allows objects to be notified of changes to specific properties of other objects. [1]

KVO is a mechanism that, once you get used to it, becomes almost invaluable. Code does not have to repeatedly poll a value to detect whether it has changed; rather, the code registers its interest in learning when the value changes and is notified when the value does change. The code is notified of the new value by way of a callback. Since Apple's KVO mechanism requires Objective-C and Cocoa, but we write games primarily in C++, I have created the KVD, a simple C++ data repository that mimics simple KVO behavior.

The KVD can take data of any type, with each piece of data having multiple observers. Observers are notified of changes immediately upon the value changing. The KVD also checks so that a value has actually changed before sending notifications, so setting a variable to the same value it currently holds will not trigger any notifications.

### 24.2 Using the KVD

As mentioned in the introduction, the KVD is designed to be used with general game state data that is read often, but changed relatively infrequently. Traditionally, game state data is repeatedly polled by lots of different systems. For example, the current screen resolution is a piece of data that changes very infrequently, but which is polled by a number of different systems. If you use the KVD to store the screen resolution, you don't need to poll for its value each frame, but you are instead told when the value changes and what the new value is.

Using an intermediary data store like the KVD can help decouple your classes and reduce header file dependencies. As in the previous example, if you were to store the current screen resolution inside the rendering system, every piece of code which is required to read or set this value needs to include the header file for the rendering system, and that could itself pull in other headers as illustrated in Figure 24.1, increasing compile times.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_488_0.png)

Figure 24.1: A polling model for accessing information often creates additional header dependencies.

Pulling the screen resolution out of the rendering system and into an intermediary would stop your game code from having to include the rendering system header (and all the headers the rendering header includes), but would add a dependency on the intermediary. As long as this intermediary header has fewer dependencies, you have simplified the header file dependency chain as shown in Figure 24.2, and this will speed up compile times.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_489_0.png)

Figure 24.2: The header dependency graph is simplified by moving information into an intermediary header.
