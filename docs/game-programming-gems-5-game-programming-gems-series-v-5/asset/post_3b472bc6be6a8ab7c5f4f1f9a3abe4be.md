
the enter, exit, and update methods as well as each link advancement conditional method. This state-specific data area is a convenient place to put timers or counters. State machines are created by asking a state machine factory for an instance of a named state machine. The state machine factory loads the file that was generated from the visual state machine data file, installs the state machine engine meta table, and returns the object to the caller. Once the caller has this table, it can begin to update the state machine. The user of the state machine factory can be another Lua script, game engine C/C++ code, or any other code for which a Lua interface exists. Once the state machine starts, the user of the state machine should run Update() at an appropriate periodic rate. If the state machine completes, Update() returns the Lua value nil, which evaluates to false in conditional statements.

## Putting It All Together

For a concrete example of this technique, let's design a state machine to operate a simple gun. The gun should be able to fire bullets, run out of ammunition, be reloaded from ammunition stored in an inventory, and perform a dry fire when there is no more ammunition left. To see the visual design, you can use UMLPad and open the file Gun1.uss from the accompanying CD-ROM; a snapshot of the state machine design is illustrated in Figure 1.15.1.

![](img/672fe9a2d008ba627b1991e15d70f43e_213_0.png)

FIGURE 1.15.1 A simple state machine describing the actions a pistol may perform.

This state machine has a beginning (the large black dot) and no end. When begun, the state machine will progress immediately to the Idle state. Because we have repurposed a general state machine editor, we must be careful to follow a few conventions when filling in the data for each state. In the Activities and Description field, the code generation script will look for the special strings OnEnter, OnExit, and OnUpdate. All text after each string will become the methods the state machine engine runs at the appropriate time. The methods will be supplied a single argument: state, which is a state-specific table that can be used to store data. If you incorporate this gem into your production pipeline, you may wish to alter UMLPad to include separate fields for each method. In the Idle state, only one method is defined: OnEnter. Every time the state machine engine progresses the state machine into the Idle state, the OnEnter method is run. In this example, the OnEnter method prints Idle to the screen.

From inspection, we can see that there are three ways for the state machine to leave the Idle state. The conditions required for advancement are detailed on each link. Every state machine update cycle, those conditions are evaluated in turn and if/when one is met, the state machine engine makes the linked state the current state, first running the OnExit method of the old current state, if it exists, then the OnEnter method of the new current state, if it exists.

In this case, pretend that triggerDown has become true because the game engine set this variable in response to the player pressing a fire button. The Firing state becomes the current state. In a real implementation, Firing's OnEnter method would probably call methods to play a gunshot sound and create an instance of a bullet in the game world. On the next update cycle, the state machine finds only one link out of the Firing state, and since there is no conditional, the link is immediately followed.

In the Recoil and Recovering state, there is also only one link out (back to the Idle state), but it cannot be followed until the timer has reached a certain threshold. Each update cycle, the state machine engine runs Recoil and Recovering's OnUpdate method, which increases the timer by the amount in frameTime, a variable set by the game engine. The rest of the state operates similarly.

## A Showcase of Data Driven Design

Running the conversion script uusToState.lua on Gun1.lua results in a file Gun1.lua that the state machine factory in StateMachineFactory.lua can use to provide gun state machines to requesting code. The script testGun.lua does just that, requesting a Gun state machine from StateMachineFactory, then simulating the role of a game engine by providing variables like frameTime, triggerDown, and reloadDown. The script testGun.lua runs the gun through the Idle, Fire, Recover, and reload states until all the ammunition is spent, then the gun falls into an endless loop of idling and dry firing.

Now comes the beauty of this gem: reconfiguration of the existing state machine to meet new design requirements. Perhaps the design department would like to do some gameplay experiments with a weapon that automatically reloads when it is out of ammunition and the trigger is released. To facilitate this, a second link from the Idle state to the Reload state with the conditional of not triggerDown and numRounds == 0 is created, and the state machine now has the desired behavior. Figure 1.15.2 shows Gun2.uss with the new link from Idle to Reload.

![](img/672fe9a2d008ba627b1991e15d70f43e_215_0.png)

FIGURE 1.15.2 A second link has been created from the “Idle” to the “Reload” state, which is followed when the gun is out of ammunition.

Compare running the Gun.lua generated from Gun1.uss and Gun2.uss through testGun.lua with reloadDown hardcoded to false to see the effect of the new behavior. The gun will reload when out of ammunition, even though reloadDown is never true. Now pretend there is a new requirement from design. The gun needs to have a 4% chance of jamming, which requires three seconds to clear. Change the Idle state to calculate a chance of jamming during each OnUpdate cycle. When the trigger is down and there are rounds to fire, if the chance to jam is less than 0.04, the state machine makes the jammed state the new state. The jammed state’s timer must be increased to three seconds before Idle becomes the current state again. We have just created two new game object behaviors with a few mouse clicks and a tiny amount of typing!

## Conclusion

Hopefully, the potential to use something besides a text editor to create in-game actions and behaviors has intrigued you. The tools and languages presented in this gem, while a good basis for beginning your experimentation with state machine code generation, are not as important as being inspired by the concept that the core structure of systems like state machines can be abstracted, written, and debugged once, then enabled by data and code provided from tools that sport a number of benefits including self documentation of systems, rapid behavior modification, enforcement of system constraints, and no specific language knowledge requirements for system designers.

## References

- [Bignami04] Bignami, Luigi. UMLPad. Available online at http://web.tiscali.it/ggb-home/umlpad/umlpad.htm.
- [Burns04] Burns, Jon and David Eichorn. "GDC 2004—Lua in the Gaming Industry Roundtable Report." Available online at http://lua-users.org/lists/lua-l/2004-04/msg00164.html.
- [Herrington03] Herrington, Jack. Code Generation in Action. Manning Publications, 2003.
- [Jerusalimschy03a] Jerusalimschy, Roberto, L. H. de Figueiredo, and W. Celes, "Lua 5.0 Reference Manual." Technical Report MCC-14/03, PUC-Rio, 2003. Available online at http://www.lua.org/manual/5.0/.
- [Jerusalimschy03b] Jerusalimschy, Roberto. Programming in Lua. Lua.org, 2003. Also available online at http://www.inf.puc-rio.br/~roberto/book/.
- [Lua04] Lua. Available online at http://www.lua.org/.
- [Manzur04] Manzur, Ariel. tolua++. Available online at http://www.codenix.com/~tolua/.

## 1.16

## A Generic Component Library

Warrick Buchanan

warrick@argonaut.com

With the increasing size and complexity of computer games, it becomes more critical that we embrace techniques that allow a more structured design methodology. The concept of viewing a software system as using a series of reusable components is not new, but it is still a practice that is not always applied where it should be within our industry.

This gem presents a configurable C++ template library that is designed to ease the process of developing reusable software components with support for features such as factories, interfaces, interface versioning, type identification policies, and reference counting.

First, we will introduce a number of elemental concepts that the library relies upon that are useful and usable separately in their own right. From these, we will build the foundation for the component system and demonstrate its use.

### Type Identification System

The library is reliant upon a means of identifying the type of a class at runtime. As there are many preferences to how one can implement a type identification system, it is presented as a configurable parameter to the library. It is a simple user-defined class that must be implemented at least in the form of:

```
struct TypeID
{
    template<class Type> TypeID(const Type* type);
    int ID();

    int operator==(const TypeID& typeID) const;
    bool operator<(const TypeID& typeID) const;

    static TypeID FromName(const char* const name);
};
```
