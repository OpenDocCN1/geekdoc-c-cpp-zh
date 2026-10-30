+   - There is another input limit, `MAX_CANON`, that we don’t show here. This limit is the maximum number of bytes in a canonical input line.
+   - Although the size of the output queue is finite, no constants defining that size are accessible to the program, because when the output queue starts to fill up, the kernel simply puts the writing process to sleep until room is available.
+   - We’ll see how the `tcflush` flush function allows us to flush either the input queue or the output queue. Similarly, when we describe the `tcsetattr` function, we’ll see how we can tell the system to change the attributes of a terminal device only after the output queue is empty. (We want to do this, for example, if we’re changing the output attributes.) We can also tell the system to discard everything in the input queue when changing the terminal attributes. (We want to do this if we’re changing the input attributes or changing between canonical and noncanonical modes, so that previously entered characters aren’t interpreted in the wrong mode.)

Most UNIX systems implement all the canonical processing in a module called the *terminal line discipline*. We can think of this module as a box that sits between the kernel’s generic read and write functions and the actual device driver (see Figure 18.2).

![](bbox=[0.428, 0.459, 0.654, 0.805])

Figure 18.2  Terminal line discipline

By isolating the canonical processing in a separate module, all terminal drivers can support canonical processing consistently. We’ll return to this picture when we discuss pseudo terminals in Chapter 19.