![](bbox=[0.182, 0.006, 0.991, 0.359])

FIGURE 4-1  SDK documentation showing namespace and assembly information for a type.

# How Things Relate at Runtime

In this section, I’m going to explain the relationship at runtime between types, objects, a thread’s stack, and the managed heap. Furthermore, I will also explain the difference between calling static methods, instance methods, and virtual methods. Let’s start off with some fundamentals of computers. What I’m about to describe is not specific to the CLR at all, but I’m going to describe it so that we have a working foundation, and then I’ll modify the discussion to incorporate CLR-specific information.

Figure 4-2 shows a single Microsoft Windows process that has the CLR loaded into it. In this process there may be many threads. When a thread is created, it is allocated a 1-MB stack. This stack space is used for passing arguments to a method and for local variables defined within a method. In Figure 4-2, the memory for one thread’s stack is shown (on the right). Stacks build from high-memory addresses to low-memory addresses. In the figure, this thread has been executing some code, and its stack has some data on it already (shown as the shaded area at the top of the stack). Now, imagine that the thread has executed some code that calls the M1 method.

![](bbox=[0.159, 0.721, 0.522, 0.915])