Even if I were a microwave designer and knew all about the inner workings of a microwave, including its software, I still wouldn't think about all those concepts while using it to heat nachos.

![](bbox=[0.13, 0.25, 0.25, 0.38])

These observations aren't profound: You can deal with only so much stress in your life. To reduce the number of issues you deal with, you work at a certain level of detail. In object-oriented (OO) computerese, the level of detail at which you're working is the level of abstraction. To introduce another OO term while I have the chance, I abstract away the details of the microwave's innards.

Happily, computer scientists — and thousands of geeks — have invented object orientation and numerous other concepts that reduce the level of complexity at which programmers have to work. Using powerful abstractions makes the job simpler and far less error-prone than it used to be. In a sense, that's what the past half-century or so of computing progress has been about: managing ever more complex concepts and structures with ever fewer errors.

When I'm working on nachos, I view my microwave oven as a box. (While I'm trying to knock out a snack, I can't worry about the innards of the microwave oven and still follow the Dallas Cowboys on the tube.) As long as I use the microwave only by way of its interface (the keypad), nothing I can do should cause the microwave to enter an inconsistent state and crash or, worse, turn my nachos — or my house — into a blackened, flaming mass.

# Preparing procedural nachos

Suppose that I ask my son to write an algorithm for how to make nachos. After he understands what I want, he can write, “Open a can of beans, grate some cheese, cut the jalapeños,” and so on. When he reaches the part about microwaving the concoction, he might write (on a good day) something like this: “Cook in the microwave for five minutes.”

That description is straightforward and complete. But it isn’t the way a procedural programmer would code a program to make nachos. Procedural programmers live in a world devoid of objects such as microwave ovens and other appliances. They tend to worry about flowcharts with their myriad procedural paths. In a procedural solution to the nachos problem, the flow of control would pass through my finger to the front panel and then to the internals of the microwave. Soon, flow would wiggle through complex logic paths about how long to turn on the microwave tube and whether to sound the “come and get it” tone.

In that world of procedural programming, you can’t easily think in terms of levels of abstraction. You have no objects and no abstractions behind which to hide inherent complexity.