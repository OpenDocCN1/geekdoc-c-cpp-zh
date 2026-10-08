
## 210 Why Classify?

(need to go back to another crack at it), but hey, an SUV is a car. As such, it shares all (or at least most) of the properties of other cars. It has a steering wheel, seats, a motor, and brakes, for example. I would bet that I could drive one without reading the user's manual first.

I don't have to clutter the limited amount of storage space in my head with all the features that an SUV has in common with other cars. All I have to remember is "An SUV is a car that . ." and on those few characteristics that are unique to an SUV (such as the price tag). I can go further. Cars are a subclass of wheeled vehicles along with other members, such as trucks and pickups. Maybe wheeled vehicles are a subclass of vehicles, which include boats and planes — and so on.

## Why Classify?

Why should you classify? It sounds like a lot of trouble. Besides, people have been using the procedural approach for a long time — why change now?

Designing and building a microwave specifically for this problem may seem easier than building a separate, more generic oven. Suppose that you want to build a microwave oven to cook only nachos. You wouldn't need to put a front panel on it, other than a Start. You probably always cook nachos for the same length of time. You could dispense with Defrost and Temp Cook nonsense in the options. The oven needs to hold only one flat, little plate. Three cubic feet of space would be wasted on nachos.

For that matter, you can dispense with the complex of "microwave oven." All you need is the guts of the oven. Then, in the recipe, you put the instructions to make it work: "Put nachos in the box. Connect the red wire to the black wire. Ring the radar tube to about 3000 volts. Notice a slight hum. Try not to stay too close if you intend to have children." Stuff like that.

The procedural approach has these problems:

- **It's too complex.** You don't need the details of nacho-building. If you can't define the objects and pull them from the morass of details to deal separately, you must deal with all the complexities of the problem at the same time.

- **It's inflexible.** Someday, you may need to replace the microwave oven with another type of oven. You should be able to do so as long as the two ovens have the same interface. Without being clearly delineated and developed separately, one object type can't be cleanly removed and replaced with another.

- **It isn't reusable.** Ovens are used to make lots of different dishes. You don't want to create a new oven every time you encounter a new recipe. Having solved a problem once, you want to be able to reuse it in other places within my program. If you're lucky, you may be able to reuse it in future programs as well.

## Object-Oriented Concept #3: Usable Interfaces

An object must be able to project an external interface that is sufficient and as simple as possible. This concept is sort of reverse of Concept #4 (described in the next section). If the device interface is insufficient, users may start ripping top off the device, in direct violation of the laws of God and society — or least the liability laws of the Great State of Texas. And believe me, you do not want to violate the laws of the Great State of Texas. On the flip side, if the device interface is too complex, no one will buy the device or no one will use all its features.

People complain continually that their DVD players are too complex, though it's less of a problem with today's onscreen controls. These devices have too many buttons with too many different functions. depending on the state of the machine. In addition, no two DVD players seem to have the same interface. For whatever reason, the DVD player projects an interface that's too difficult and nonstandard for most people to use beyond the bare basics.

Compare the VCR with an automobile. It would be difficult to argue that a car is less complex than a VCR. However, people don't have much trouble driving cars.

All automobiles offer more or less the same controls in more or less same place. For example, my sister once had a car (need I say a French car?) that had the headlight control on the left side of the steering wheel, where the turn signal handles normally lives. You pushed down on the light lever to turn off the lights, and you raised the lever to turn them on. This difference may seem trivial, but I never did turn left in that car at night without turning off the lights.

A well-designed auto doesn't use the same control to perform more than one operation, depending on the state of the car. I can think of one exception to this rule: Some buttons on cruise controls are overloaded with multiple functions.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_236_0.png)

## Object-Oriented Concept #4: Access Control

A microwave oven must be built so that no combination of keystrokes you can enter on the front keypad can cause the oven to hurt you. Certainly, some combinations do not anything. However, no sequence of keystrokes de

- **Break the device:** You may be able to put the device into a strange state in which it doesn't do anything until you reset it (say, by throwing an internal breaker). However, you shouldn't be able to break the device using the front panel — unless, of course, you threw it to the ground in frustration. The manufacturer of this type of device would probably have to send out some type of fix for it.

- **Cause the device to catch fire and burn down the house:** As bad as may be for the device to break itself, catching fire is much worse. We live in a litigious society. The manufacturer's corporate officers would likely end up in jail, especially if I have anything to say about it.

However, to enforce these two rules, you may have to take responsibility. You can't make modifications to the inside of the device.

Almost all devices of any complexity, including microwave ovens, have a small seal to keep consumers from reaching inside them. If the seal is broken, indicating that the cover of the device has been removed, the manufacturer no longer bears responsibility. If you modify the internal work of an oven, you're responsible if it subsequently catches fire and burns down the house.

Similarly, a class must be able to control access to its data members. No sequence of calls to class members should cause your program to crash. The class cannot possibly ensure control of this access if external elements have access to the internal state of the class. The class must be able to keep critical data members inaccessible to the outside world.

## How C# Supports Object-Oriented Concepts

Okay so does C# implement object-oriented programming? In a sense, this is the wrong question. C# is an object-oriented language; however, it doesn't implement object-oriented programming — the programmer does. You can certainly write a non-oriented program in C# or any other language (by, for instance, writing all of Microsoft Word in Main()) comes to mind. Something like “you can lead a horse to water” But you can easily write an object-oriented program in C#.

These C# features are necessary for writing object-oriented programs:

- **Controlled access:** C# controls the way in which class members can be accessed C# keywords enable you to declare some members open to the public whereas internal members are protected from view and some secrets are kept private.Notice the little hints. Access controls are revealed in Chapter 5 of this minibook.

- **Specialization:** C# supports specialization through a mechanism known as inheritance. One class inherits the members of another class. For example, you can create a Car class as a particular type of Vehicle. C# specializes in specialization.

- **Polymorphism:** This feature enables an to perform an operation it wants to. The Rocket type of Vehicle may implement the Start operation much differently from the Car type of Vehicle does. At least, I hope it does every time I turn the key in my car. (With my car, you may not know) But all Vehicles have a Start operation, and you can rely on that Chapter 7 in this minibook finds its own way of describing polymorphism.

- **Indirection:** Objects frequently use the services of other objects — by calling their public methods. But classes can "know too much" about the classes they use. The two classes are then said to be "too coupled," which makes the using class too dependent on the used class. The design is too brittle — liable to break if you make changes. But change is inevitable in software, so you should find more indirect ways to connect the two classes. That's where the C# interface comes in. (You can get the scoop on interfaces in Chapter 8 of this minibook.)
