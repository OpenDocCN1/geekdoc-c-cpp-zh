```
int damage =
    (this.DamageClass - target.ArmorClass) * r.Next(20);
    target.CurrentHitPoints -= damage;
}
}
}
```

In Listing 3.9 there are a couple of minor changes to the access modifiers for some of the class members, and we have the implementation of the Attack and MoveTo methods. What you might notice is that the CurrentHitPoints property now has an access modifier of internal for the set accessor. This means that only classes within the same Assembly as Combatant are able to modify that property. This allows your “game engine” to freely tweak combatant health but does not allow code outside the core engine to modify that data directly. This forces all changes to hit points to go through only authorized routes.

Additionally, the Location property now has a private access modifier. This means that only the Combatant class itself can modify its own location. This forces changes to the Combatant’s location to go through the MoveTo method, which is the only acceptable means for moving a Combatant.

The reason I mention these here is because C# has much finer-grained control over access modifiers for methods and members than Objective-C, allowing you to place much more firm control over which code can and cannot affect certain pieces of data. Although this might seem like an unimportant detail, it becomes incredibly important when you are writing code that other developers will consume. An entire type of “accidental side effect” bugs can be eliminated by preventing unwanted changes to your member variables and properties.

# Inheritance

In this section of the chapter we’re going to take a look at how we can use inheritance to create specialized derivatives of the original Combatant class. For example, we might want to create a particular type of combatant that cannot move, such as an automated turret or a stationary cannon. Another kind we might want to create might be combatants that get an extra attack because they are so quick. Finally, we might want to create something completely unusual, such as a drunken attacker who never hits for more than one point of damage at a time.

Figure 3.1 shows the class hierarchy diagram that we want to create from the existing Combatant class. As you can see, we want to create three new classes:

+   - ReallyDangerousCombatant
+   - StationaryCombatant
+   - DrunkenCombatant