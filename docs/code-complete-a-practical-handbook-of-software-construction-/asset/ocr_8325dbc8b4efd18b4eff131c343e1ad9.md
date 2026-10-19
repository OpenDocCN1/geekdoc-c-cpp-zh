As you can see, every subsystem ends up communicating directly with every other subsystem, which raises some important questions:

+   - How many different parts of the system does a developer need to understand at least a little bit to change something in the graphics subsystem?
+   - What happens when you try to use the business rules in another system?
+   - What happens when you want to put a new user interface on the system, perhaps a command-line UI for test purposes?
+   - What happens when you want to put data storage on a remote machine?

You might think of the lines between subsystems as being hoses with water running through them. If you want to reach in and pull out a subsystem, that subsystem is going to have some hoses attached to it. The more hoses you have to disconnect and reconnect, the more wet you’re going to get. You want to architect your system so that if you pull out a subsystem to use elsewhere, you won’t have many hoses to reconnect and those hoses will reconnect easily.

With forethought, all of these issues can be addressed with little extra work. Allow communication between subsystems only on a “need to know” basis—and it had better be a good reason. If in doubt, it’s easier to restrict communication early and relax it later than it is to relax it early and then try to tighten it up after you’ve coded several hundred intersystem calls. Figure 5-5 shows how a few communication guidelines could change the system depicted in Figure 5-4.

![](bbox=[0.232, 0.546, 0.679, 0.769])

**Figure 5-5.** With a few communication rules, you can simplify subsystem interactions significantly.

To keep the connections easy to understand and maintain, err on the side of simple intersubsystem relations. The simplest relationship is to have one subsystem call routines in another. A more involved relationship is to have one subsystem contain classes from another. The most involved relationship is to have classes in one subsystem inherit from classes in another.