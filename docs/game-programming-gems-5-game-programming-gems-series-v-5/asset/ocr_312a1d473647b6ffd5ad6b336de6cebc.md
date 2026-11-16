to the render component asking the Entity component for the object's world position. Any of the code in the game that has access to the object manager can query for an interface belonging to a particular object. All that is needed is the object ID.

The second means of communication between components comes in the form of messages. This is useful for the situation where a component has something to say, but does not quite know to whom to say it. A message can be sent to an object or to all objects. In the case of the collectable component telling the object it belongs to that it is picked up and wants to be hidden, it would post a message to all the components in the object to say that it would like to be hidden. Each component type will tell the object manager at initialization time which messages it is interested in receiving.

# Extending Our Object

So what to do if we want to be able to bend the spoon? At the moment, our spoon object is rigid and does not bend easily. The solution is simple enough: we add an animation component to the object.

Now, we have not really talked about how objects are defined. That bit seemed easy in the traditional system: the object was defined by where it was in the inheritance tree and by the methods it exposed to the rest of the world. We could still make a class for each object type and use aggregation so that each object class is built up from a bunch of has-a relationships rather than the is-a relationships of old. This brings us one step closer to what we want, but it still means that objects are set up in code, and that means we need to compile every time we change the structure of an object.

What we would really like to have is the whole process of creating objects be completely data driven. That way, designers can play around with existing objects and even create new object types without any programmer input. The system has everything that is needed to make this happen. We simply need to derive file formats for specifying components and objects and provide the designers with the tools they will need.

# Creating the System

Now that we have a reasonable idea of what we want, we can go ahead and create the system. The companion CD-ROM has all the code for a component-based object management system, including a few different components and messages to get started using it. It is not a complete system, and there is not really any way that it can be considering that all games are different, but it should be easy enough to extend the system to make it work for a wide range of games.

![](bbox=[0.12, 0.73, 0.18, 0.76])

# The Component Interface

The first class that we are going to have a look at is the component interface. This is the class from which all other component interfaces and components derive. It looks like this: