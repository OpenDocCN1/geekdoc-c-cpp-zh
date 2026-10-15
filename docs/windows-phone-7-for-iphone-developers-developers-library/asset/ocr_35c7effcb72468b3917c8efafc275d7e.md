true). Several design patterns are violated by these giant if statements, but in the interest of keeping things simple in this chapter, I won’t go into their names or definitions here.

To sum up: If you can solve your specialization issues with inheritance and interfaces (discussed in the next section), that is often a much cleaner, more maintainable and reliable solution than filling a single “bloat master” class with inordinate amounts of properties and logic.

# Programming with Contracts

Contracts are different from class implementations. A contract merely defines the requirements of a particular class; it does not actually control the class implementation. To continue the combatant analogy: A Combatant base class defines behavior that all child classes can inherit. A Combatant contract defines the behavior and data that must be implemented by any class wanting to call itself a combatant.

Let’s walk through an example while assuming we’re still building a game engine. If we go with a straight inheritance hierarchy, we might be limiting the types of interactions we can model. Assuming single inheritance (which is the case for both Objective-C and C#), anything that can do damage to a player (via the Attack method) must inherit from Combatant. This presents us with a problem: What about complex inanimate objects with a unique inheritance hierarchy but that cannot inherit from Combatant?

Let’s say the player is walking through an alley and is struck by a car. Vehicles in this game might require their own inheritance hierarchy, probably starting with a base class such as Vehicle or MovingObject. Given that we don’t have the capability to do multiple inheritance, how do we allow noncombatant objects to do damage to players without messing up the Combatant object hierarchy? The answer is contracts.

Contracts are called protocols in Objective-C and interfaces in C#, but they serve identical purposes. Contracts define a minimum set of required properties or methods that must be implemented by a particular class. They do not enforce any restrictions on inheritance hierarchies. It is critically important here to remember that two classes, each with entirely different inheritance hierarchies, can implement the same interface.

So let’s take a look at the Combatant class. The Attack method does two things (which might give us a clue that we can start refactoring there): It figures out how much damage to do to an opponent, and then it asks the other combatant to take that damage. If we take out the function of taking the actual damage and make that a requirement on an interface called ITakesDamage, we start getting some real flexibility in our game engine. This interface has a requirement that anything implementing that interface must implement a method called TakeDamage.

Listing 3.15 shows the ITakesDamage interface in C#, and Listing 3.16 shows the new Combatant class, refactored to separate out the concern of doing damage to be something that satisfies the interface requirement.