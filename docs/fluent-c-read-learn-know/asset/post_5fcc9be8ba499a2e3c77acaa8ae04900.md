
## REVIEW

Now that you've seen the keywords, can you place each of the snippets below on the continuum from most abstract to most concrete?

- 1. public void DoSomething()
- 2. public abstract MyBase
- 3. public abstract void DoSomething()
- 4. public virtual void DoSomething()
- 5. public sealed MyClass
- 6. public sealed override DoSomething()

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_431_0.png)

## TAKE A BREAK

Wow, this chapter was a doozy, wasn't it? Why don't you take a break before you complete the final Review and move on to the next chapter on programming principles?

abstract

This keyword returns a Boolean value indicating whether a variable can be cast to the specified type.

Inheritance

This keyword allows a method to be overridden in an inheriting class.

is

This term indicates the ability of one type to inherit state and behavior from another.

Abstraction

sealed

This keyword returns a variable cast to the specified type, or null if that's not possible.

Encapsulation

static

This keyword marks a method or class that must be inherited.

Polymorphism

The term refers to the ability of a type to be treated as one of the types from which it derives.

as

virtual

This term refers to the general principle of leaving out unnecessary details.

This keyword marks a method as belonging to the entire class, not an instance.

This term refers to the ability to use a method or class without knowing the details of its implementation.

This keyword prevents a class or method from being inherited.

## Congratulations! You've finished the chapter. Take a minute to think about what you've accomplished before you move on to the next one...

List three things you learned in this chapter:

- 1
- 2
- 3

Why do you think you need to know these things in order to be a C# programmer?

Is there anything in this chapter that you think you need to understand in more detail? If so, what are you going to do about that?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_434_0.png)

## PROGRAMMING PRINCIPLES

In the last chapter, we looked at some of the theory behind designing object-oriented applications, specifically how the relationships between types can be defined and implemented. It’s probably obvious that understanding the mechanics of an object-oriented design in that way is necessary, but it’s only part of the picture.

The design principles we’ll look at in this chapter address a basic fact of the programming life: It’s gonna change. Nobody is ever going to ask an architect to insert three floors in the middle of the Empire State Building, but it happens to programmers all the time. So think of this chapter as a kind of self-defense course for programmers. The principles we’ll explore will help you build an object model that’s resilient to change (which is programmer-speak for “it won’t break more when you fix it”).

Common wisdom says that any given application will spend four times as long being changed as it will being developed in the first place, and studies have shown that 80% of that maintenance effort will be spent modifying the behavior of the application, not fixing errors.

Yikes. Better be ready for it, hadn’t we?

> WORDS FOR THE WISE
> 
> “There’s no difference between theory and practice in theory. There’s a lot of difference between theory and practice in practice.”
> 
> Vaguely attributed to the inimitable Yogi Berra, the computer scientist Jan van de Snepscheut and Albert Einstein.

### FITTING IT IN

In the last chapter we examined the basic principles of Object-Oriented Analysis & Design. In this chapter we'll continue that exploration by examining four of the classic design principles.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_436_0.png)

We'll talk about architectures and patterns in Chapter 14.

In this chapter we'll explore four classic design principles.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_437_0.png)

### SMELLY CODE

One of the best ways to learn to write good code is to learn how to recognize bad code. Code that doesn't work is obviously bad, but there are other hallmarks. Most programmers call these Code Smells. There are lots of them (there's an infinite number of ways for anything to be not-quite-right), and every theorist seems to list them differently, but here are a few to get you started:

### RIGIDITY

If changing one piece of code requires changes to another piece, which might then require changes to a third piece, and..., the code is rigid. And smelly.

### FRAGILITY

Cynical programmers (that is, anybody who's done it for a living) say that there are always three bugs in any application: the one you know about, the one you don't know about, and the one you're going to create when you fix the one you know about. Fragile code breaks in unexpected ways, in areas that don't seem to be related to what you're working on.

### IMMOBILITY

A common situation: You're modifying an application, and you want to re-use a bit of code. But the snippet you need is so tightly entrenched that the only way to re-use it is to cut and paste. You're looking at code that's immobile. That's a smelly waste of time.

### REDUNDANCY

Immobile code is the primary cause of this design smell. When you're programming, some kinds of lazy are good. If there's any bit of code that appears in more than one place, you've got a smelly problem, because if the snippet needs to change (and it will), you need to change it everywhere. How do you spell "boring"?

### OPACITY

I really wish I had money for every time I've seen a comment like "Don't know how this works, but it does" in a release application. I don't need to tell you that this is unacceptable, right? If you don't understand it, how are you going to know how to change it? You should write code that makes comments seem unnecessary. (But comment everything anyway.) If you need the comment to understand the snippet, then your code is opaque, and opacity smells. Really, really badly.

## IF IT AIN'T BROKE...

On a slow news day, the American press is fond of regaling us with stories of military overspending. Remember the $640 toilet seat or the $7,600 coffee maker? Now I'm not privy to the Department of Defense's procurement procedures, but I'd bet I know how those things happen: When you're not certain what constitutes "good enough", the safe bet is to substitute "best", and that almost always means "most expensive you can find". It's not unreasonable, really, but it can (and all too frequently does) result in embarrassing over spending.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_438_0.png)

The same thing applies to software design. The principles we'll explore in this chapter come at a price, both in initial design and development time, and in application complexity. That price isn't always justified. (Would you buy a Formula I race car just to go to the grocery store? Well, you might if you're a petrol-head, but could you justify the expense to the IRS or worse, to your spouse?)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_438_1.png)

So what's a poor programmer to do? When you're evaluating your design, ask yourself two questions:

- - Does this class (or class member) violate one of the design principles?
- - Does it matter?

That second question is the critical one. For example, most of the principles we'll be exploring in this chapter are aimed at reducing the cost of maintenance. But a surprising number of applications aren't maintained; they're replaced.

Even when you're developing an application that you expect to be in service for some time, the added complexity of implementing all the principles rigidly may not be justified, because some things just don't change. So, here's a way of going forward. It's not ideal, but it works in the real world.

- 1. Review your initial design in light of the design principles.
- 2. If you find that a class violates a principle, consider how expensive fixing it now would be. If it's a simple change, you should implement it now.
- 3. If bringing the class into compliance with the principle is going to add a lot of complexity, consider how likely it is to change. If the class seems to you to be volatile, implement the change.
- 4. If, on the other hand, the class doesn't seem particularly volatile, document the changes required, but don't implement them until (and unless) the class actually does change during maintenance.
