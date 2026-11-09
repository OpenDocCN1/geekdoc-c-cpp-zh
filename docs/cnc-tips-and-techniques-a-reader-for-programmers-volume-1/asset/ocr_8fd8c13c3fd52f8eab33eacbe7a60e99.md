# # Threading Methods Compared

![](bbox=[0.097, 0.111, 0.169, 0.146])

*September 2005, updated February 2013*

When it comes to single point threading on CNC lathes, part programmers have several choices — three, in fact. The oldest programming method was, and still is, a method that is also very time consuming. This is the original block-by-block threading, using preparatory command G32 (also known as G33 on some controls). Because of the many calculations required to prepare even a few simple threading passes, it did not take long for the control developers to make the programming process a little shorter, and the first threading cycle was born. This cycle is still known today by its preparatory command G92. Although a significant improvement for its time, the G92 cycle has not met the high expectations of part programmers and machine operators. Finally, Fanuc has come up with a true gem — the G76 multiple repetitive threading cycle. A bit of a mouthful for a description, G76 has quickly become the king of single point threading. How does that position the other threading methods, using the G32 and G92 commands? Is there still room for them?

# ## The G32 Method

The G32 method of thread cutting is also known as the “long hand” method — and long it can be. The most fundamental understanding of G32 is that it is not a cycle of any kind. It is a plain programming of each and every step in the threading process. Take a typical single pass of a thread; it has four parts. From the start position, the tool will rapid to the diameter to be threaded, then the threading itself will take place. Next, the tool has to retract away from the thread and, finally, it must return back to the start position.

These four parts represent four blocks of the program. With seven passes, for example, the threading motions will only take twenty eight blocks of the program. For the best results, each