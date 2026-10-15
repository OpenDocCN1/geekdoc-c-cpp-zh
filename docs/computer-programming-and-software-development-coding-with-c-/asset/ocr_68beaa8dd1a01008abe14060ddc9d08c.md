![](bbox=[0.12, 0.07, 0.91, 0.25])

I cannot distinguish between these two. But that's not what I was planning on doing; I actually added the third parameter, and that's okay for C#. So now just including a third parameter of type integer, in this case, bonus, and I used that inside of my method. So these two methods are not overloaded methods. They have the same name but a different number of parameters. But I can also do the same thing, but the difference now is that the parameter types are different, so they're now doubles.

![](bbox=[0.12, 0.51, 0.91, 0.6])

So at this point, C# can still distinguish between these three methods based on the parameters, the number of parameters, or the types of parameters that I'm passing it. So I'm going to go here, and I'm going to bring in a bonus. Let's set that to 1000. I'm going to change the method invocation as we already had, and I'm going to add bonus. You see automatically that Visual Studio is showing me these overloads.