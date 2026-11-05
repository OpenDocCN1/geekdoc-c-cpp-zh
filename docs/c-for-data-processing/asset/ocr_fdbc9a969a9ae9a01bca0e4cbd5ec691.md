This method does nothing, but it does do it many millions of times. If I run a program that calls this method the first thing that happens is that the program seems to stop. Then the fan in my laptop comes on as the processor starts to heat up as it is now working hard. If I start up Windows Task Manager I see the picture below:

![](bbox=[0.35, 0.26, 0.5, 0.42])

My laptop has four processor cores, which means that it can run four threads at a time. You can see little graphs under the CPU (Central Processor Unit) Usage History part of the display showing how busy each processor is. From the look of the above graph, the leftmost processor and the rightmost processor are quite busy but the middle two processors are not doing anything. If I stop my program running I get a display like the one below.

![](bbox=[0.35, 0.55, 0.5, 0.7])

Now all the processors are just ticking over. When we start using more than one thread we should see more of the graphs climbing up, as my programs run on multiple processors.

# Programmer's Point: Multiple Threads Can Improve Performance

If you can work out how to spread your program over several threads this can make a big difference to the speed it runs at. The method above can only ever use a maximum of 25% of my system, since it only runs on one of the four available processors.

# 5.6.4 Running a Thread

An individual thread is managed by your program as an instance of the Thread class. This class lives in the System namespace. We have used namespaces to locate resources before when we used files. The easiest way to make sure that we can use all the threading resources is to add a using directive at the start of our program:

```
using System.Threading;
```

The Thread class provides a link between your program and the operating system. One job of the operating system is to manage threads on your computer and decide