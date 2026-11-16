This solves our problem (for now) but also introduces new problems. Now, all collectable objects have become animating objects because one of the classes that derived from `CollectableObject` needed animation. That is quite a lot of baggage for a lot of objects to carry around. It also means that our poor health pack and any other collectable objects have to implement any pure virtual methods from `AnimatingObject` just to be valid objects, even if those methods do not make sense for those objects.

Now let us consider what happens if we want to allow objects to take damage. We should only need a couple of methods to be able to do that, so we decide to add those methods to an existing class. Our design calls for objects deriving from the `CActor` class to take damage (these are not shown here but would typically include at least `CPlayer` and `CEnemy`/`CAICharacter`), so we go ahead and add the methods to `CActor`. This seems like a sensible choice.

As time goes on, it is decided that doors are supposed to be able to take damage and be destroyed as well. To give them the ability to do so, the damage methods are moved up to `CAnimatingObject`, as that is the first common ancestor of `CActor` and `CDoor`. It seems like a reasonable decision, and it gives us what we want. Another reasonable decision might be to move the damage methods up to `CRenderableObject` if a non-animating object needs the ability to take damage. The effect of a lot of these "reasonable" decisions is that our tree becomes increasingly top-heavy. A class high up the tree also ends up with a lot of methods that are not there because of what the class does but because of where it is in the tree. Such classes lose their cohesion as they try to be all things to all objects.

# Components

We have seen that we run into quite a few problems if we rely on all objects being part of a big inheritance tree. What we would really like instead is a system where we can combine existing functionality into new objects and add new functionality to existing objects without having to refactor a lot of code and reshuffle the inheritance tree every time we want to do so.

# A Simple Object

A good solution is to create an object from component parts. A component is a class that contains all the data members and methods used for a particular task. An object is in turn built up by composing several components together. Figure 1.3.3 shows a spoon object and the components from which it is made.

The Entity component allows us to place the object in the world. The Render component allows us to associate a model with the object and render it according to the settings of that component. The Collectable component allows us to pick up the object and keep it in our inventory.