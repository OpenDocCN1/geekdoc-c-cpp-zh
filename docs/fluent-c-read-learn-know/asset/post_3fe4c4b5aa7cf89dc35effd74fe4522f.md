
## FITTING IT IN

In this chapter we'll complete our exploration of the principles of software development by examining some of the most important design patterns, and also take a quick look at the architectural patterns that you can use to organize complex applications.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_468_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_468_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_468_2.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_468_3.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_468_4.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_468_5.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_468_6.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_468_7.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_468_8.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_468_9.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_468_10.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_468_11.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_468_12.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_468_13.png)

Architectural patterns define how the different parts of an application work together.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_469_0.png)

The Observer pattern is used for .NET events.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_469_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_469_2.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_469_3.png)

### WHY PATTERNS?

- PATTERNS ARE PROBLEMS SOMEBODY ELSE HAS ALREADY SOLVED.

> When I'm developing a new recipe, it may look like I'm just randomly throwing things in, but whether it's a chowder or a new kind of fruit pie, there's always a classic technique that I use to structure the dish.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_470_0.png)

- PATTERNS ARE STRUCTURES YOU CAN WORK WITHIN TO SOLVE YOUR PROGRAMMING PROBLEMS.

### PATTERNS GIVE YOU A WAY TO TALK ABOUT YOUR PROGRAMS.

> I'd like you to take a slice of bread and put it in front of direct heat until it's just lightly brown. Then turn it over and do the same thing on the other side. And could I have some butter and jam to go with it, please?

> Why didn't he just ask for toast?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_471_0.png)

### TASK LIST

There are many more design principles than the few we looked at in the last chapter, and there are more design patterns than we'll be able to cover here. I've picked a few that you'll see a lot when you're working with the .NET Framework. They should give you a taste for what design patterns are and how they work.

### THE STRATEGY PATTERN

We'll start this chapter off by exploring the Strategy pattern (which looks a lot like programming to interfaces) and how it can help us refine our type hierarchies.

### THE OBSERVER PATTERN

Next we'll examine observers, subjects, and the events that bind them in the Observer pattern, one of the most important patterns in the .NET platform.

### ARCHITECTURAL PATTERNS

Design patterns typically address problems in the way that objects interact. Application architectures, while not technically design patterns, address similar types of problems with the way application components interact. We'll examine the Layered Architecture, one of the most sophisticated and flexible, in some detail.

### PRESENTATION PATTERNS

Finally, we'll return to design patterns with a look at the Model-View based patterns that are used to structure the user interface.

### THE STRATEGY PATTERN

I have a surprise for you. (I hope it's a good one.) You already know the first of the design patterns we're going to be exploring.

When we were examining DEPENDENCY INVERSION in the last chapter, we saw that it's often implemented by a technique called “programming to interfaces”, which looks like this:

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_473_0.png)

That's the basic structure of the STRATEGY PATTERN. There is one little twist, though: The pattern is technically only the Strategy when it represents some behavior of the ClientClass (not just an object the ClientClass works with.)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_473_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_473_2.png)

### USING STRATEGY

We've learned from our chefs that different categories of baked goods change their yield using different methods. If we use inheritance for all the different possibilities, we're going to have a problem:

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_474_0.png)

Using classical inheritance, we'd create a lot of classes that differ only slightly. It's easy to see how the class hierarchy could get really cluttered really quickly. (There are different categories of cakes and bread, for example, each of which would need a different class.)

The other problem here is that if the semantics of the ChangeYield() function changes (say, for example, you decide that you need another parameter), you have to fix it in lots of different places. That's potentially a lot of repetitive work. Who needs that?

Using the Strategy pattern, we still have as many classes (in fact, we have an extra type), but we gain two things: flexibility and a simple mechanism for re-using behaviors.

The RecipeBase class now has a property called YieldBehavior that takes an instance of IYieldBehavior. Because it's declared in the base, it will be inherited by each of the concrete recipe types.

The ChangeYield() method in the base class simply needs to call the ChangeYield method of the behavior:
YieldBehavior.ChangeYield();

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_475_0.png)

The classes that inherit from RecipeBase can decide at runtime what their YieldBehavior is. The appropriate behavior can be assigned in the constructor, and changed at any time.

Initially we've added an extra interface class to the hierarchy, so it probably doesn't seem any simpler. But think about what happens when, say cupcakes need to re-use the CakeYieldBehavior? No new code, just an assignment. That's the real power of the STRATEGY pattern.

### STRATEGY DEFINED

### STRATEGY

Define a family of algorithms, encapsulate each one, and make them interchangeable. Allow the algorithm to vary independently from the clients using it.

### THE PROS

- Code re-use: Multiple types can use the same algorithm.
- Simplified hierarchy: Strategy eliminates classes that only vary by behavior.
- Runtime flexibility: Strategy allows objects to change their behavior at runtime.
- Simpler maintenance: If an algorithm changes, it need only be changed in the behavior class that represents it.

### THE CONS

- If algorithms aren't being changed or re-used, Strategy can add more complexity to the class hierarchy than it removes.

### TAKE A BREAK

The Strategy pattern is pretty simple once you understand it, but it's fundamental to modern OOA&D. Why don't you take a break before completing the exercise and we move on to a pattern that's very important in the .NET Framework: the Observer.

### PUT ON YOUR THINKING HAT

Most recipes share the same preparation method, so the PreparationSteps collection in our recipe hierarchy could also benefit from the Strategy pattern. Can you change the hierarchy so that recipes have a PreparationMethod. (For the exercise, create a method class for soup and one for bread.)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_477_0.png)

Write a constructor for BakedGoodRecipe that uses the preparation method class for bread.

### HOW'D YOU DO?

It doesn't matter if you chose different names for the objects in your hierarchy.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_478_0.png)

```
public void BakedGoodRecipe()
{
    this.PreparationMethod = new BreadMethod();
}
```

### MAKE A NOTE

Strategy is useful in three situations:

- Multiple classes implement the same behavior.
- Sub classes vary only by behavior.
- A class can change its behavior at runtime.

### THE OBSERVER

Think about the way a restaurant works

> How do you think you could translate this to a class hierarchy?

The Kitchen Can do the thing listed on the menu.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_479_0.png)

The Customer lets the Kitchen know what to do by telling the Waiter, who passes the order on to the Kitchen.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_479_1.png)

The Customer wants one or more of the items on the menu.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_479_2.png)

When the order is ready, the Kitchen tells the Waiter, who delivers it to the Customer.

Now, the interesting thing, here (from an OOA&D point of view, which is quite different from that of a restaurant critic) is that the Kitchen doesn't know about the Customer, and the Customer doesn't know much about the Kitchen except what's on the menu. The Waiter knows about the Kitchen and the Customer, but doesn't need to know how the food is prepared.

The Customer only knows what the Kitchen Can do, but needs to know when their food is ready.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_479_3.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_479_4.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_479_5.png)

The Kitchen doesn't know anything about Customers: it just does stuff, and lets the Waiter know when it's done.
