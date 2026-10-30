This is an example of the Template Method pattern, in which an algorithm is modeled but its general steps are customizable because of delegation to abstract methods. In effect, the base class delegates the individual steps of the process to subclasses.

These methods need not be abstract; they could be virtual. The difference here is mainly the granularity of what has been made extensible. Rather than replacing the ProcessTrades method in its entirety, you can now replace select parts of the process by overriding the constituent methods.

# Interface inheritance

The final type of extension point discussed in this chapter is the alternative to implementation inheritance: interface inheritance. Here, the client's dependency on a class is replaced with the now-familiar delegation to an interface. Figure 8-4 shows the client's dependency on the interface and the two implementations of the interface.

![](bbox=[0.08, 0.49, 0.68, 0.78])

FIGURE 8-4 The client depends on an interface rather than a class.

Interface inheritance is preferable to implementation inheritance. With implementation inheritance, all subclasses—present and future—are clients. This prevents modification because, with implementation inheritance, subclasses depend on the implementation, too. All implementation changes are thus potentially client-aware changes. This echoes the advice to prefer composition over inheritance and to keep inheritance hierarchies shallow, with few layers of subclassing. If a change is made to add a member at the top of the inheritance graph, that change affects all members of the hierarchy.

Interfaces are also better extension points because they can be decorated with rich object graphs of functionality that touch upon many different contexts. They are more flexible than classes. I don't mean that the virtual and abstract methods that form the extension points of class inheritance are not useful, but that they do not provide quite the same level of adaptability as do interfaces.