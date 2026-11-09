# # Preventing Scrap with Offsets

*May 2008, updated February 2013*

![](bbox=[0.063, 0.101, 0.152, 0.143])

The major goal of a CNC operator should always be to make any part to drawing specifications. At the same time, the operator should also make an effort to prevent making a scrap. It is not uncommon to scrap a few small pieces made of a long bar before making the perfect part. This leisurely approach often leads to complacency and may prove costly when the number of blank parts is fixed.

# ## Methods for Preventing Scrap

There are only a few reasons for scrap to happen in the first place. On the human side, it is either negligence or incompetence. On the machine side, it is a hardware or software failure. Needless to say, the human errors happen more often. There are several ways CNC programmers and operators can prevent a scrap. Some procedures have to be included in the program; others can be done at the machine directly. Programmers often include extra features in their programs that help to eliminate scrap. Typical methods are:

+   - Providing a trial cut, using block skip function or some other method
+   - Including *Program Stop/Optional Stop* functions M00/M01
+   - Including messages or comments
+   - Making a setup sheet with a sketch
+   - Splitting a tool motion for single block operation
+   - Programming sufficient clearances

These are just some of the methods that can be built into the program to make it easier for the operators. CNC operators also have several ways to prevent a scrap created from any cause. They must identify a potential problem before it becomes a real problem. The first goal is to be able to interpret the program and know what it does. Mistakes made during tool or fixture setup are a common cause of scrap. Errors also happen during data