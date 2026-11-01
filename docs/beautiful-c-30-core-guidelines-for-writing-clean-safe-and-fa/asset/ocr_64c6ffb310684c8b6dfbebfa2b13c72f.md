Guidelines, wrote an article titled “The Free Lunch Is Over.”² He highlighted the problem with Moore’s Law, predict-ing the necessity of a hard turn toward concurrency in software to exploit the full potential of upcoming CPUs with increasing numbers of cores. He observed the lack of understanding of concurrency among most programmers, and how efficiency and optimization would become more important than ever.

2. www.gotw.ca/publications/concurrency-ddj.htm

Cramming more and more transistors onto a processor was no longer an option for achieving faster compute speeds. At around the end of 2006 I encountered my first dual-core processor. Processors might not be able to get faster, but they could do more things at once, which is just as good, right?

Of course it isn’t. Two cores only execute your code twice as fast if they are not waiting for each other. My heart sank a little. I knew what was coming and I was not disappointed. Race conditions and deadlocks became part of the life of a developer as we tried to squeeze more and more out of the processor. I had become comfortable with I/O threads: now the world was filling up with compute threads. Multithreaded programs have become the new normal, particularly in my domain of games. Proces-sors with dozens of cores are common. Core Guideline CP.1: “Assume that your code will run as part of a multi-threaded program” acknowledges this truth.

# Avoiding deadlocks and data races

Deadlocks and data races are caused by breakdowns in turn-taking. Two threads are competing for a single resource: access to a piece of data. That is the motivation for this guideline. If writable data is not shared, then races and deadlocks will not be a problem. Unfortunately, threads need to communicate with one another. What is needed is a way of reading and writing data with a guarantee of no interference from other threads.

C++11 introduced std::atomic, a library type that supports this. Particularly, if one thread writes to an atomic object while another thread reads from it, the behav-ior is well defined, and all is well with the world. But what happens if two threads want to write to the object? Now we need