# Multi-Start Threading

*May 2007, updated February 2013*

![](bbox=[0.06, 0.108, 0.148, 0.149])

For most threading applications on a CNC lathe, a thread is programmed with a single start. Programmers do not even think about the thread as having one start, they just take it for granted. The majority of threads in this category are designed for fasteners, such as bolts and nuts. Threads are also used for the purpose of transferring a motion, rather than for fasteners. Although these threads can also have only a single start, there are many that require more than one start. These are called multi-start threads, and they require special attention in programming.

# The Theory of Multi-Start Threading

In order to transfer a motion rapidly over a relatively long distance, two, three, four, or more starts multiply the speed of motion. For example, take a standard external thread with eight threads per inch (8 TPI). It takes eight revolutions to travel one inch. With a double start, it takes only four revolutions, and with four starts, only two revolutions are required. Of course, a coarser thread can be used for the same result, but at a price — the thread depth will increase dramatically. Keeping the thread depth constant while speeding up the motion is the major reason for using multi-start threads.

In programming, the often misused term pitch must be understood as the distance between two adjacent threads — nothing else. Another term, the lead of a thread, takes on a special importance. Lead is the amount of axial travel in one revolution of the thread. For single start threads, pitch and lead are the same, hence the misuse of terminology. It is important to understand that the feedrate per revolution for threading is always the lead, never the pitch.

Take a single start thread of 8 TPI. Its lead and pitch are both 0.125, so the feedrate is F0.125. If the drawing specifies the thread