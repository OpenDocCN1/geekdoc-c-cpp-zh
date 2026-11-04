To see the effect of resuming execution, press F10 to single-step from the point where we hit the breakpoint. This moves the main thread to the closing curly brace on its for loop. Notice, though, the background thread also got unfrozen, and there's a chance (because you're dealing with timing, there are no certainties) the background thread made progress while execution was resumed for the very short time it took to single-step over the Console.WriteLine call. Figure 29.12 shows this effect, where it's clear the background thread made progress during the single-stepping we've done.

![](bbox=[0.07, 0.32, 0.78, 0.68])

FIGURE 29.12 Analyzing debugger behavior with regard to thread execution.

Why do I consider this to clearly be the case? Just look at the time deltas in the output for the thread with ID 9. From this, you can see that I stayed in the debugger for about 14 seconds after hitting the breakpoint. During that time, the background thread didn't make any progress. However, upon hitting F10, this background thread had a chance to run and printed another message. This all happened while the debugger was waiting for the main thread (with ID 8) to complete the single-stepping, which took us beyond the Console.WriteLine call, explaining the last message.

# Freeze and Thaw

While debugging multithreaded issues, you often want to do some “what if” analysis to get to the bottom of the observed behavior. Suppose, for example, that a whole bunch of threads are dealing with the same underlying resource and you observe that resource going bad one way or another. To pinpoint the source of the problem, you want to narrow down the problem to the thread that's improperly doing its synchronization duties.

Although there’s no perfect way to do such analysis, I want to point out some tools that can help. One is the debugger’s capability to freeze and thaw threads. When you freeze a thread, it remains suspended until you issue the thaw command on the thread, which enables you to eliminate a thread from the global picture you’re trying to get to of the misbehaving program. If the problem you’re debugging suddenly disappears, that can be a pretty good indication of the frozen thread being at fault.