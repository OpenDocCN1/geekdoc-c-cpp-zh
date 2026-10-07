# The Abstraction: Address Spaces

In the early days, building computer systems was easy. Why, you ask? Because users didn't expect much. It is those darned users with their expectations of “ease of use", “high performance", “reliability", etc., that really have led to all these headaches. Next time you meet one of those computer users, thank them for all the problems they have caused.

# 13.1 Early Systems

From the perspective of memory, early machines didn't provide much of an abstraction to users. Basically, the physical memory of the machine looked like what you see in Figure 13.1 (page 130).

The OS was a set of routines (a library, really) that sat in memory (starting at physical address 0 in this example), and there would be one running (a process) that currently sat in physical memory (starting at physical address 64k in this example) and used the rest of memory. There were few illusions, and the user didn't expect much from the OS. Life was so easy for OS developers in those days, wasn't it?

# 13.2 Multiprogramming and Time Sharing

After a time, machines were expensive, people began to share machines more effectively. Thus the era of multiprogramming was born [DV66], in which multiple processes were ready to run at a given time, and the OS would switch between them, for example when one decided to perform an I/O. so increased the effective utilization of the CPU. Changes in efficiency were particularly important in those days where machine cost hundreds of thousands or even millions of dollars (and you thought your Mac was expensive!).

Soon enough, however, people began demanding more of machines, and the era of time sharing was born [59, L60, M62, M83]. Specifically, many the realizations of batch computing, particularly on programmers themselves [CV65], who were tired of long (and hence ineffec-