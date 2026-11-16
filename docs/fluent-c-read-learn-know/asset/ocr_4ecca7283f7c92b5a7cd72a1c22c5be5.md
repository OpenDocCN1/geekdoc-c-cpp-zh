# # WHAT IF...?

Our use case describes an ideal interaction between the user and the system. That’s great, but we all know that the world hardly ever runs according to plan, and a resilient system can’t ignore that. So in addition to the ideal case, you’ll need to capture what could go wrong (as best you can), and what the system should do when it does. Think of them as Murphy’s Law cases...

In our simple example, the ingredient the user is looking for might not be on the list. Or there might be a system problem. For example, the database containing the ingredients and suppliers might not be available at runtime. What should the system do when these things happen?

Alternate paths through the system aren’t always the result of problems, of course. Sometimes the user just needs to do something a little differently. Whatever their source, these alternate paths should be captured as part of the use case. Our revised version looks like this:

![](bbox=[0.09, 0.52, 0.9, 0.88])