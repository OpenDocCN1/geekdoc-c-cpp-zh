# # Threading

When computers first came out they all had a CPU, a processor if you like, and for those of you who don't know, this is the computer’s brain. These days, modern computers have two or more processors and each one may well be hyperthreaded, which makes it feel like you have double the amount of power. Some of the top computers can have eight, even 16 processors and some of them can be linked so that other computers are working for yours too, which gives you an almost unlimited amount of processing power.

What has all this got to do with C# programming? This – most computers have an incredible amount of power but when we run a C# program, we run on one processor and that wastes an awful lot of computing power.

We're going to be looking at a feature called threading. With the basic process, we can take pieces of code that are all independent of one another and get them running in different 'threads'. A thread is pretty much like its own program in that your computer will run several at the same time on all the different processors in the system. Just to clear things up, the one thing a thread isn't is its own program because it still has to share memory with whatever program or process that created it.

When multiple threads are running simultaneously, your computer will allow one or more, depending on how many your system has, thread run for a little while before switching it out for another one suddenly. The computer decides the time for the switch and it decides which thread is being switched, but it does this quite efficiently so we don't need to worry too much about that.

The most important thing to know at this stage is that several threads can run simultaneously and it is down to the operating system to determine when they get switched about and with which thread. They are all treated much the same but they all get switched about on occasion and this randomness can cause a few problems at times – we’ll cover this in Thread-safety.