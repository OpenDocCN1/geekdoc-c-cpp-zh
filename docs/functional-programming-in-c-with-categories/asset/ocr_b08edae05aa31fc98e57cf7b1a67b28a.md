# Category Theory

# Endofunctor

A Functor from a category to itself is called an endofunctor. Given any category C, we can create a new category End(C) is called the endofunctor category of C. The objects of End(C) are endofunctors F:C → C, and the morphisms are **natural transformation** between such endofunctors.

In a visual form this would look like the following. First, we have a functor Between the same Category **C**. Since this section is more abstract, I am not going to give a programming example just yet. Let’s first say that we have this category C that has some Objects and arrows (we omit the arrows here).The objects are just those three ●, ●, ●

![](bbox=[0.375, 0.327, 0.725, 0.467])

The functor F transforms the green ●→● the purple ●→● and the red ●→●

But since the object are the same, we could depict it in the same diagram.

![](bbox=[0.375, 0.568, 0.595, 0.708])

Now we can place this F as a point in the Category of Endofunctors where the Objects are Functors in C