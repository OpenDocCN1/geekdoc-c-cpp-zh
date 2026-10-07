# CHAPTER 4
Cocoa Design Patterns

later or extend those variable parts without affecting the other parts of the system. You eliminate dependencies and reduce couplings between parts, and consequently the system becomes more flexible and easier to change.

Benefits such as make design patterns an important consideration when you're writing software. If you find, adapt, and use patterns in your program's design, program—and the objects and classes that it comprises—will be more reusable, more extensible, and easier to change when future requirements demand it. Moreover, programs that are based on design patterns are generally more elegant and efficient than programs that are, as require fewer lines of code to achieve the goal.

# An Example: The Command Pattern

Most of the book by the Gang consists of a catalog of design patterns. It categorizes the patterns in the catalog by scope (class or object) and by purpose (creational, structural, or behavioral). Each entry in the catalog describes the intent, motivation, applicability, structure, participants, collaborations, consequences, and implementation of a design pattern. One of these entries is the Command pattern (an object-behavioral pattern).

The book states the intent of the Command pattern as "encapsulate a request as an object, thereby letting parameterize clients with different requests, queue them, and support undoable operations." The pattern separates sending a message from the objects that receive and evaluate those messages. The originator of the message (the client) encapsulates a request by binding one or more operations on a specific receiver. The encapsulated message can be passed around between objects, placed in queues or otherwise stored for later invocation, and dynamically modified to vary the receiver or message parameters.

Figure 4-1 Structure diagram for the Command pattern

![](bbox=[0.176, 0.546, 0.822, 0.728])

For a developer with Cocoa, this short overview of the Command pattern might ring a bell. The pattern perfectly describes a class in the Foundation framework whose purpose is to encapsulate messages: NSInvocation. As the pattern's intent, one of its purposes is to make operations undoable. Invocation objects are used in the Cocoa designs for undo management as well as distributed objects, which is an architecture for interpersonal communication. The Command pattern also describes (less perfectly) the target-action mechanism of Cocoa in which user-interface objects encapsulate the target and action of the messages they send when users activate them.