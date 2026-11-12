# Alternatives to ECS

To understand why the ECS is a smart choice for building our game engine, we must first look at the alternatives. We are going to look at the object-oriented design, component-oriented design, and data-oriented design. Our comparison will be done using the following categories:

+   - Performance and Maintenance
+   - CPU Cache and Memory Usage

# Object-Oriented Design

On the surface, it appears that object-oriented (OO) programming is an excellent choice for creating games because games are simply a collection of objects interacting in a scene. This design, however, has numerous flaws that have caused many game developers to abandon it.

![](bbox=[0.19, 0.37, 0.81, 0.63])

A typical OO design for a game will look like the picture above. On top of we have an interface Object that contains pure virtual functions like update(), destroy(), render() that must be implemented by all child classes like GameObject and UIObject. The picture above shows the tree level of inheritance which means we also have three levels of virtual lookup-table. This can have a massive impact on performance as the processor will have to look up the table to find the proper function to call.

In the image above, we have a child class called Player as well as another one called Boss. What if we want a Boss who is also a Player? This is where things get strange with the OO design because we'll have to use multiple inheritances, which is already a bad idea as it would make it even more difficult to maintain.

Since all objects must inherit from the "Object" interface, we must allocate