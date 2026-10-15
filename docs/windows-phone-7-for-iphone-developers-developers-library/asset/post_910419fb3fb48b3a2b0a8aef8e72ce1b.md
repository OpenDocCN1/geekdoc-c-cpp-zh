
## Adding Behavior

Now that you’ve got a class that encapsulates data, you want to add behavior to it. Behavior in classes is added in the form of methods, which are functions that execute within the scope of an instance of a class.

Methods in Objective-C typically have their signature defined in the header (.h) file and the implementation defined in the implementation (.m) file. In C#, the method is defined directly on the class and there is no header used for exposing the method signature.

Some of the behavior that we want to add to our Combatant class might include attacking another combatant and moving. Listings 3.7 through 3.9 illustrate how we go about adding methods to the class to give our class some behavior. A good general rule is to think of members (or properties) as nouns on a model, whereas behaviors (or methods) should be considered verbs on a model.

### Listing 3.7 Combatant.h with Behavior

```
@interface Combatant : NSObject {
}

- (void)attack:(Combatant *)target;

@property(nonatomic, assign) int maxHitPoints;
@property(nonatomic, assign) int currentHitPoints;
@property(nonatomic, assign) int armorClass;
@property(nonatomic, assign) int damageClass;
@property(nonatomic, retain) NSString *combatantName;
```

Listing 3.7 shows the header for the Combatant class, including the property declarations as well as a method signature for the Attack method.

### Listing 3.8 Combatant.m with Behavior

```
#import "Combatant.h"

@implementation Combatant
@synthesize maxHitPoints, currentHitPoints, armorClass, damageClass, combatantName;

- (void)attack:(Combatant *)target
{
    // obviously this should be more complicated...
    target.currentHitPoints -= rand() % 20;
}
@end
```

Listing 3.8 shows the Objective-C implementation of the Attack method. This method operates on a supplied instance of another combatant to allow it to do damage to the other target. It’s important to keep in mind here that in Listing 3.8’s Objective-C code and in Listing 3.9’s C# code, both classes are using encapsulated accessors to manipulate the other objects; they are not modifying internal variables directly.

### Listing 3.9 Combatant.cs with Behavior

```
using System;
using System.Net;
using System.Windows;
using System.Diagnostics;

namespace Chapter3
{
    public class Combatant
    {
        public int MaxHitpoints { get; set; }
        public int CurrentHitPoints { get; internal set; }
        public int ArmorClass { get; set; }
        public int DamageClass { get; set; }
        public string Name { get; set; }
        public Point Location { get; private set; }

        public int HitPointPercent
        {
            get
            {
                double pct =
                    (double)CurrentHitPoints / (double)MaxHitpoints;
                return (int)Math.Floor(pct * 100);
            }
        }

        public void MoveTo(Point newLocation)
        {
            this.Location = newLocation;
            Debug.WriteLine("Combatant {0} just moved to ({1},{2})",
                this.Name,
                this.Location.X,
                this.Location.Y);
        }

        public void Attack(Combatant target)
        {
            Random r = new Random();
            // obviously oversimplified algorithm...
```
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

## Inheritance

In this section of the chapter we’re going to take a look at how we can use inheritance to create specialized derivatives of the original Combatant class. For example, we might want to create a particular type of combatant that cannot move, such as an automated turret or a stationary cannon. Another kind we might want to create might be combatants that get an extra attack because they are so quick. Finally, we might want to create something completely unusual, such as a drunken attacker who never hits for more than one point of damage at a time.

Figure 3.1 shows the class hierarchy diagram that we want to create from the existing Combatant class. As you can see, we want to create three new classes:

- ReallyDangerousCombatant
- StationaryCombatant
- DrunkenCombatant

![](img/04a00d46bb1059867d95707babd62ee7_41_0.png)

Figure 3.1 Class inheritance hierarchy diagram.

Building these classes in either C# or Objective-C is pretty straightforward. C# gives us a bit more fine-grained control over what the inheriting types can do and see, so we’ll make more use of the access modifiers than we do in Objective-C.

In Listings 3.10 and 3.11, I show a sample derivative class called ReallyDangerousCombatant, written in Objective-C, that does double damage. This is inheritance in its most basic form—creating a child class that provides behavior that supersedes that of the parent.

### Listing 3.10 ReallyDangerousCombatant.h

```
#import "Combatant.h"

@interface ReallyDangerousCombatant : Combatant {
}
@end
```

And the implementation of the “really dangerous” combatant class:

### Listing 3.11 ReallyDangerousCombatant.m

```
#import "ReallyDangerousCombatant.h"

@implementation ReallyDangerousCombatant

- (void)attack:(Combatant *)target
{
    [super attack:target];
    target.currentHitPoints -= 12;
}
```

In Listing 3.11, you can see that the really dangerous combatant first asks its parent class (indicated by the super keyword) to attack the target. Then it does its own damage to the target. This really dangerous implementation will always do 12 more damage than a regular combatant would do because of the inheritance hierarchy.

In the interest of saving space and spending more time focusing on the C# implementations of these classes, I won’t include the listings for DrunkenCombatant.h, DrunkenCombatant.m, StationaryCombatant.h, and StationaryCombatant.m. The following three listings show the C# implementations for the new derived classes.

### Listing 3.12 ReallyDangerousCombatant.cs

```
namespace Chapter3
{
    public class ReallyDangerousCombatant : Combatant
    {
        public override void Attack(Combatant target)
        {
            base.Attack(target);

            // attack again for good measure!
            base.Attack(target);
        }
    }
}
```

Listing 3.13 shows how we can use inheritance and child classes to make a combatant that is so drunk it can’t possibly win a fight and has an incredibly hard time moving where the game tells it to move:

### Listing 3.13 DrunkenCombatant.cs

```
using System;
using System.Windows;

namespace Chapter3
{
    public class DrunkenCombatant : Combatant
    {
        public override void Attack(Combatant target)
        {
            target.CurrentHitPoints -= 1; // never do any real damage
        }

        public override void MoveTo(Point newLocation)
        {
            Random r = new Random();
```
