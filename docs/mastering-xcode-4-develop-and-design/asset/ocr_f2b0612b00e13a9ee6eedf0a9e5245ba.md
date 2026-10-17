# AN OVERVIEW OF DTRACE

DTrace lets you trace your application as it runs. Tracing is logging information about a running computer program for debugging and performance analysis; it is used mainly by developers. Contrast this with “high-level logging,” which is used by end users and system administrators to log program errors, exceptions, failed scripts, and so on.

Apple added DTrace support and debuted Instruments in Mac OS X 10.5. Instruments reduces the DTrace learning curve to manageable levels and makes a lot of traditionally difficult debugging tasks seem almost trivial by comparison.

In DTrace, a probe is a script to perform a specific task. In the glossy, graphic realm of Instruments, a probe (or collection of interrelated probes) is more generally referred to as an instrument. A probe is essentially a script that watches for specific events and records relevant information.

In the field of quantum mechanics, it’s been shown that the act of observing something changes its nature. This is true of profiling software as well. For example, adding a bunch of code to an application to track its performance will affect its performance. One of the most celebrated aspects of DTrace is its extremely minimal performance impact when a probe is enabled; and there is no impact for disabled probes. This means that for most developers, the act of tracing won’t have a noticeable impact on the application’s performance profile. Because of this, DTrace can be used on production systems without slowing them down.

TIP: You can run DTrace from the command line by using the dtrace command. Type man dtrace in the Terminal and press Return to learn more.

![](bbox=[0.0, 0.42, 0.27, 0.75])