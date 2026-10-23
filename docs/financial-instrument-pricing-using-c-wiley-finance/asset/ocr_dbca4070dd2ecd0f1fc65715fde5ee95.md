+   - Facade: create a unified interface to a logical grouping of objects or subsystems.
+   - Adapter: convert the interface of one class into the interface of another otherwise incompatible class.
+   - *Behavioural patterns*: how objects send messages to each other:
+     - Visitor: extend the functionality of a class hierarchy (non-intrusively).
+     - State: implement a Harel/UML statechart (Harel and Politi, 2000).
+     - Strategy: create flexible, interchangeable algorithms for object methods.
+     - Observer: define synchronising procedures between objects.
+     - Mediator: define a single communication ‘hub’ in a star of objects.
+     - Command: encapsulate a request.

We remark that the GOF design patterns can be viewed as a special case of an LCM because we are interested in object lifetime; the main phases are the creation of an object (MAN), placing the object in some structure (RAT) and then monitoring how the object interacts with other objects in the object network (MIS).

# 9.3 SYSTEM SCOPING AND INITIAL DECOMPOSITION

In general, we try to understand as much of the problem as possible before delving into detailed design and coding work. To this end, our goal is to reduce *project risk* by locating the boundaries of the problem. In this way we must know what needs to be developed. Second, we decompose the initial amorphous (‘ball of mud’) and monolithic system into loosely coupled and autonomous systems with well-defined interfaces.

We need to be careful not to fall into the trap of *premature design and implementation*; our concern here is to understand the main data flow in the system and how the different systems partaking in the context diagram cooperate to realise that data flow.

# 9.3.1 System Context Diagram

The first step in understanding a software system is to describe the system (henceforth called SUD (*System Under Discussion*)) in terms of external systems where the inputs come from and where the outputs from the system go to, respectively.

We define the crucial concepts of *source* and *sink* boxes (DeMarco, 1978):

> > A source or sink is a person, organisation or software system that lies outside the context of the SUD system and that is a net originator or receiver of system data, respectively.

It is obvious that we need to understand what a system’s major sources and sinks are before proceeding. To this end, we represent the system context diagram by a drawing in which each system is depicted as a rectangular box with lines connecting the SUD with its sources and sinks. Even at this stage we would like (if possible) to distinguish between those external systems that must be included in the design (that is, those that must be implemented by the developer) and those that we do not design and for which we are only interested in the services that they provide or require with respect to the SUD. To this end, we add a single vertical line to those boxes representing the former category and no line for the latter category. The SUD is