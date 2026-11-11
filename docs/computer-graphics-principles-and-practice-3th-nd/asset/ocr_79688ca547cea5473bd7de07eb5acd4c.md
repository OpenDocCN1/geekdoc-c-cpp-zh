![](bbox=[0.091, 0.107, 0.648, 0.419])

Figure 35.17: Four images of animated characters autonomously performing complex tasks requiring motion planning. (Courtesy of the Graphics Lab at Carnegie Mellon University. ©2004 ACM, Inc. Reprinted by permission.)

![](bbox=[0.717, 0.107, 0.925, 0.23])

Figure 35.16: An interpolated leg position between key poses found by one of the earliest inverse kinematics algorithms. (Courtesy of A.A. Maciejewski. ©1985 ACM, Inc. Reprinted by permission.)

![](bbox=[0.717, 0.348, 0.925, 0.546])

Figure 35.18: Complex global flocking behaviors (top) emerge in Reynolds's seminal “boids” animation system [Rey87] from simple, local rules for each virtual bird (bottom). (©1987 ACM, Inc. Included here by permission.) (Courtesy of Craig Reynolds, ©1987 ACM, Inc. Reprinted by permission.)

![](bbox=[0.091, 0.497, 0.647, 0.59])

Figure 35.19: A complex traversal requiring both pathfinding and general motion planning [SH07]. (Courtesy of Jessica Hodgins and Alla Safonova ©2007 ACM, Inc. Reprinted by permission.)

drawers must be opened before the clothes could be taken out. Figure 35.17 shows some examples of “simple” daily tasks that represent complex planning challenges for virtual characters.

A special case of motion planning is the task of navigating through a virtual world. At a high level, this is simply pathfinding for a single character. When there are enough characters to form a crowd, the multiple-character planning problem is more challenging. Creating the phenomenon of real crowds (or herds, or flocks ... ) is surprisingly similar to simulating a fluid at the particle level, with global behavior emerging from local rules as shown in Figure 35.18.

When the space to be traversed does not admit a character's default method of locomotion, the pathfinding problem is of course much harder. For example, the character in Figure 35.19 must not only find a path, but also decide when to crouch and when to jump to avoid obstacles on the desired path while satisfying physical constraints on the body.