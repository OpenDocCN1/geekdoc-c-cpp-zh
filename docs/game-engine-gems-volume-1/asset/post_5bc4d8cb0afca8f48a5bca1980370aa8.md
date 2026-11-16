
### 22.4 The Future of Task Parallelism in Games

Established habits of game development have been disrupted by the installed base of multi-core CPUs. In the same way, game development will be disrupted again by the introduction and evolution of powerful many-core processors that require special programming techniques in order to be used effectively. With the techniques discussed in this gem, you'll be able to create task parallelism abstractions that will get your game running quickly in any parallel hardware environment.

### References

[1] Jérôme Muffat-Mérido."Do-it-yourself Game Task Scheduling". Intel Software Network, 2009. http://software.intel.com/en-us/articles/do-it-yourself-game-task-scheduling/

[2] Intel Threading Building Blocks. http://www.threadingbuildingblocks.org/

## Chapter 23: Dynamic Code Execution Hierarchies

Martin Linklater

Sony Studio Liverpool

### Overview

As hardware becomes more complex and powerful, the software that they run becomes larger and more complex. As software grows, the number of programmers needed to write and maintain the software increases. As anyone who has experienced large programming teams will tell you, the more programmers you have working on one product, the more time you need to spend policing the code structure and managing its complexity.

As different programmers create and modify game systems, it is easy for the code to become a mismatch of different patterns and styles. Programmers also tend to have their own personal preferences when it comes to object creation, initialization, updating, and deletion.

Inter-object communication, if not tightly regulated, can become a spaghetti of code dependencies and object graph traversals. As programmers build objects that require data from other objects, it is all too easy to create monolithic dependency graphs and be forced to navigate awkward and non-intuitive object linkages. It is also too easy to create header file dependencies that have nothing to do with the actual job you are trying to accomplish, but are required so you can connect to other objects in the code.

Keeping track of code construction can become a full-time job, and modifying the code during the latter stages of a project can become error prone and dangerous. Fragile code is difficult to bug-fix without causing more bugs.

This gem discusses code execution hierarchies (CEH) as a way of controlling these problems and visualizing your code when things get confusing.

### 23.1 What are Code Execution Hierarchies?

Code execution hierarchies provide a framework for code construction and updating. You use a simple base class for all of your major game components, and define the update order by way of a manager class with an internal tree structure. Rather than create objects and add them manually to the main loop, as in Figure 23.1(a), you create your objects and attach them to the execution tree relative to an already existing object. Conceptually, the structure is similar to a scene graph in graphics programming where each object has a parent, and the object's location in the scene is always defined relative to its parent. When you move or update a node in the graph, all of its children are automatically moved with it, maintaining the parent-child relationships. The main loop using a code execution hierarchy is shown in Figure 23.1(b).

![](img/7ba1225bb0e5a87be0fd35866408ffa7_475_0.png)

Figure 23.1: (a) Traditional update loop. (b) Code execution hierarchy.

Explicitly defining the parent-child and sibling relationships of your code modules not only forces people to *think* before adding an object to the update system (always a good thing), but also helps protect your code from structural changes in the future. If a code module needs to be updated somewhere else during the frame, you move the parent, and the child objects are automatically moved along with it.

A simple base class is used for execution objects so that the manager class has a consistent API interface for your objects. This base class also defines the API for object creation, initialization, updating, and deletion. Runtime type identification systems provide a simple way for objects to identify themselves within the hierarchy. This is used when objects need to find objects of a certain type within the hierarchy. A simple base class may look like that shown in Listing 23.1. Objects can be created and added to the hierarchy as shown in Listing 23.2. Rather than building your code explicitly and defining your update order in the main loop, you are creating code objects and inserting them into the code execution hierarchy.

### Listing 23.1: Example base class.

```
class CEHBase
{
    public:
        CEHBase();
        virtual ~CEHBase();

        virtual void Init(void);
        virtual void Update(float dt);
        virtual void ... grab the latest code and pru

    protected:
        m_classID;
};
```

### Listing 23.2: Example game code.

```
MyObj *obj = new MyObj;
obj->Insert(kAsChildOf, kRootNode);
obj->Init();

OtherObj *other = new OtherObj;
other->Insert(kAsSiblingAfter, obj);
other->Init();
```

### 23.2 Design Features

#### Tree Structure

The object hierarchy itself is a tree structure. There is one root node, owned by the manager class. Each object has one and only one parent. Each object has zero or more siblings, and each object can have one child link. Once you have your tree structure, there are two relationships that are required to be maintained when parsing the tree:

- Parents are always updated before their children.
- Siblings are always updated in the same order, first to last.

Given these two relationships, there are two ways to traverse the tree and update your objects: depth first and breadth first. Which one you choose depends on your requirements, but due to memory access patterns and performance I favor the breadth-first traversal. Figures 23.2 and 23.3 show a simple graph and the update orders for both systems. As you can see, the two rules above are maintained for both traversal systems—previous siblings are processed before next siblings, and parents are processed before children. A real-world example of a CEH might look like that shown in Figure 23.4.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_478_0.png)

Figure 23.2: Simple graph.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_479_0.png)

Figure 23.3: Update orders.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_479_1.png)

Figure 23.4: Example CEH Graph.

#### Time Deltas

You may have noticed that the `Update()` method in the base takes a floating-point `dt` parameter. This is used to tell your object how much time has elapsed since the last call to `Update()`. Making your code flexible regarding update frequencies and decoupling objects from V-sync events can have great benefits, as long as you are willing to do the extra work to make your object internals robust for varying `dt` values.

Adding awareness of time also gives your CEH the potential to deal with varying timing requirements for its objects. For instance, it is simple to build basic timer functionality into the manager class, allowing you to specify how often various objects require updating. If you have an object that only needs to be updated approximately once each second, then that object can tell the manager that its desired update interval is only every second. The manager class can then handle the update call for you.

#### Dynamic Structure

Since the update hierarchy is built at run time, it can be treated as a dynamic data structure. Update order is not hardwired into your code, but can be modified and altered as required. If network code does not need to be updated due to there being no network connection, you simply omit it from the update graph. This can be much cleaner than placing the following if statements all over your code.

```
if (networkActive)
{
    ...blah...
}
```

It also allows you to define your update graph via a data file, allowing runtime behavior to change without recompiling your code.

#### Introspection

By building an introspection system into your CEH base class you allow for much more flexible code construction. I'm sure we've all been in the position of needing to get a handle on a certain class instance and being forced to navigate a lot of run-time linkage to get at the object. The alternative is to make the desired object global, rarely a good thing. As an example, in Figure 23.2, for object E to get a pointer for object G, it could be required that E goes through code like this:

```
ptrG = GetD() ->GetA() ->GetB() ->GetF() ->GetG();
```

This is rather clunky, and if the linkage of intermediate classes changes, say objects A and B are swapped, all of the code that manually navigates the linkages needs to be updated.

Using a CEH with introspection, the call could look like this:
