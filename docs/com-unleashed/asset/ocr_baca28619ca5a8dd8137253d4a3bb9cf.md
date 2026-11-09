Although the client holds on to the object reference, it is bound to the assigned server. During the entire lifetime of the object reference, the assigned server maintains the object and all related activities. When the client finally releases the reference (with a call to `Release()`), the unit of work ends. Figure 20.1 shows this process.

# **FIGURE 20.1**  
*An overview of request routing.*

![](bbox=[0.324, 0.206, 0.899, 0.416])

Granularity is a relative measure of how small a unit of work is. A finer degree of granularity indicates fewer tasks for each unit of work. A coarser degree of granularity indicates more tasks for each unit of work. That means that an object with a fine degree of granularity is instantiated with `CoCreateInstance()`, but then does very little, and can only make a handful of method calls. It is then destroyed with a call to `Release()`. An object with a coarse granularity starts with a `CoCreateInstance()` and ends with a `Release()`, but probably makes many method calls (or at least makes method calls that consume large amounts of time and energy).

# Parallelism Illustrated

To illustrate granularity, let me present both extremes. On one side we have a very finely grained object that makes a single method call between the time it’s created and the time it’s released. On the other side is a coarsely grained object that remains alive for weeks, in which time thousands or millions of method calls are made.

You’re probably asking which one is better in a situation when good load balancing is desired. The answer is, “It depends.”

It should be pretty obvious that the most even load balancing can be achieved with fine granularity. Let’s say you have an application that’s composed of coarsely grained objects. Client requests are satisfied, and everything is well-balanced. But the client machines might stay connected for days or weeks. If this is the case, then you are vulnerable to some of the same weaknesses that stall load balancing has. The load can become