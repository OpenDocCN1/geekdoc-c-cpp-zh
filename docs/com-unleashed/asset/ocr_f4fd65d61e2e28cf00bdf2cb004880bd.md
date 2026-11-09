the reasons that smaller, discreet components work better because of the load time of the component being shorter. Many classes, even if they are simple, in a VB project produce larger compiled components. For MTS and COM+, this is bad. It’s better to have more smaller components; in fact, in VB they should be compiled for small size preferred over faster code.

You can’t throw away OO principles. They have tremendous merit. When your application grows into a huge enterprise application, OO is a good thing because of the organization it provides. But you can’t forget performance and the resource issues, either. Everything I do now is a balance of the two. I keep things object-oriented when I can, and don’t worry so much about OO architecture when it hurts performance and resource allocation past an unacceptable level.

# The Right Language for the Job

Obviously you must decide on a language with which to develop a component. Visual Basic allows for quick and robust component development. Visual C++ takes longer, is more prone to bugs, but gives better performance. I haven’t used Visual J++ in any real-life settings, but may choose it for a variety of tasks. (Visual J++ was usually chosen because it is very easy to develop components with, and unlike Visual Basic, it is truly object-oriented.)

# Avoid Middle Tier State

To achieve scalability and performance, you shouldn’t use stateful components. Specific issues exist with using the Session and Application objects to store state of any kind. Not the least of these issues is the current inability to scale such objects across multiple servers. This becomes especially problematic (even in single-server deployments) when someone attempts to cache object instances, such as database connections in Session or Application objects.

# Avoid Data Access in the Middle Tier

Developers (especially those under a tight deadline) sometimes directly perform tasks on data from the middle tier where the business logic resides. I know that rules can be hard and inflexible, and there are times when they should be broken, but it would be unusual to find a justification for breaking this one. Direct data access in a middle tier while in a Windows DNA application is likely to perform more poorly than it would otherwise.

For example, it would be a mistake to retrieve multiple data sets from different tables and then join, sort, or search the data in middle-tier objects. The database is designed to handle this kind of activity, and moving it to a middle tier is almost certainly a bad practice. True, there might be circumstances in which doing so is called for because of the