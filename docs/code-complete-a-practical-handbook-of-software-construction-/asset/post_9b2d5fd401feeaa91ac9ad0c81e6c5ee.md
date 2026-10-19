
- *Replace inheritance with delegation* If a class needs to use another class but wants more control over its interface, make the superclass a field of the former subclass and then expose a set of routines that will provide a cohesive abstraction.
- *Replace delegation with inheritance* If a class exposes every public routine of a delegate class (member class), inherit from the delegate class instead of just using the class.
- *Introduce a foreign routine* If a class needs an additional routine and you can't modify the class to provide it, you can create a new routine within the client class that provides that functionality.
- *Introduce an extension class* If a class needs several additional routines and you can't modify the class, you can create a new class that combines the unmodifiable class's functionality with the additional functionality. You can do that either by subclassing the original class and adding new routines or by wrapping the class and exposing the routines you need.
- *Encapsulate an exposed member variable* If member data is public, change the member data to private and expose the member data's value through a routine instead.
- *Remove Set() routines for fields that cannot be changed* If a field is supposed to be set at object creation time and not changed afterward, initialize that field in the object's constructor rather than providing a misleading Set() routine.
- *Hide routines that are not intended to be used outside the class* If the class interface would be more coherent without a routine, hide the routine.
- *Encapsulate unused routines* If you find yourself routinely using only a portion of a class's interface, create a new interface to the class that exposes only those necessary routines. Be sure that the new interface provides a coherent abstraction.
- *Collapse a superclass and subclass if their implementations are very similar* If the subclass doesn't provide much specialization, combine it into its superclass.

### System-Level Refactorings

- *Create a definitive reference source for data you can't control* Sometimes you have data maintained by the system that you can't conveniently or consistently access from other objects that need to know about that data. A common example is data maintained in a GUI control. In such a case, you can create a class that mirrors the data in the GUI control, and then have both the GUI control and the other code treat that class as the definitive source of that data.
- *Change unidirectional class association to bidirectional class association* If you have two classes that need to use each other’s features but only one class can know about the other class, change the classes so that they both know about each other.
- *Change bidirectional class association to unidirectional class association* If you have two classes that know about each other’s features but only one class that really needs to know about the other, change the classes so that one knows about the other but not vice versa.
- *Provide a factory method rather than a simple constructor* Use a factory method (routine) when you need to create objects based on a type code or when you want to work with reference objects rather than value objects.
- *Replace error codes with exceptions or vice versa* Depending on your error-handling strategy, make sure the code is using the standard approach.

## CHECKLIST: Summary of Refactorings

### Data-Level Refactorings

- Replace a magic number with a named constant.
- Rename a variable with a clearer or more informative name.
- Move an expression inline.
- Replace an expression with a routine.
- Introduce an intermediate variable.
- Convert a multiuse variable to multiple single-use variables.
- Use a local variable for local purposes rather than a parameter.
- Convert a data primitive to a class.
- Convert a set of type codes to a class or an enumeration.
- Convert a set of type codes to a class with subclasses.
- Change an array to an object.
- Encapsulate a collection.
- Replace a traditional record with a data class.

### Statement-Level Refactorings

- Decompose a boolean expression.
- Move a complex boolean expression into a well-named boolean function.

- **Keep refactorings small** Some refactorings are larger than others, and exactly what constitutes “one refactoring” can be a little fuzzy. Keep the refactorings small so that you fully understand all the impacts of the changes you make. The detailed refactorings described in *Refactoring* (Fowler 1999) provide many good examples of how to do this.
- **Do refactorings one at a time** Some refactorings are more complicated than others. For all but the simplest refactorings, do the refactorings one at a time, recompiling and retesting after a refactoring before doing the next one.
- **Make a list of steps you intend to take** A natural extension of the Pseudocode Programming Process is to make a list of the refactorings that will get you from Point A to Point B. Making a list helps you keep each change in context.
- **Make a parking lot** When you’re midway through one refactoring, you’ll sometimes find that you need another refactoring. Midway through that refactoring, you find a third refactoring that would be beneficial. For changes that aren’t needed immediately, make a “parking lot,” a list of the changes that you’d like to make at some point but that don’t need to be made right now.
- **Make frequent checkpoints** It’s easy to find the code suddenly going sideways while you’re refactoring. In addition to saving the code you started with, save checkpoints at various steps in a refactoring session so that you can get back to a working program if you code yourself into a dead end.
- **Use your compiler warnings** It’s easy to make small errors that slip past the compiler. Setting your compiler to the pickiest warning level possible will help catch many errors almost as soon as you type them.
- **Retest** Reviews of changed code should be complemented by retests. Of course, this is dependent on having a good set of test cases in the first place. Regression testing and other test topics are described in more detail in Chapter 22, “Developer Testing.”
- **Add test cases** In addition to retesting with your old tests, add new unit tests to exercise the new code. Remove any test cases that have been made obsolete by the refactorings.
- **Review the changes** If reviews are important the first time through, they are even more important during subsequent modifications. Ed Yourdon reports that programmers typically have more than a 50 percent chance of making an error on their first attempt to make a change (Yourdon 1986b). Interestingly, if programmers work with a substantial portion of the code, rather than just a few lines, the chance of making a

**Cross-Reference** For details on reviews, see Chapter 21, “Collaborative Construction.”

### Bad Times to Refactor

> Do not partially write a feature with the intent of refactoring to get it complete later.  
> —John Manzo

> A big refactoring is a recipe for disaster.  
> —Kent Beck

- **Don’t use refactoring as a cover for code and fix** The worst problem with refactoring is how it’s misused. Programmers will sometimes say they’re refactoring, when all they’re really doing is tweaking the code, hoping to find a way to make it work. Refactoring refers to changes in working code that do not affect the program’s behavior. Programmers who are tweaking broken code aren’t refactoring; they’re hacking.
- **Avoid refactoring instead of rewriting** Sometimes code doesn’t need small changes—it needs to be tossed out so that you can start over. If you find yourself in a major refactoring session, ask yourself whether instead you should be redesigning and reimplementing that section of code from the ground up.

## 24.5 Refactoring Strategies

The number of refactorings that would be beneficial to any specific program is essentially infinite. Refactoring is subject to the same law of diminishing returns as other programming activities, and the 80/20 rule applies. Spend your time on the 20 percent of the refactorings that provide 80 percent of the benefit. Consider the following guidelines when deciding which refactorings are most important:

- **Refactor when you add a routine** When you add a routine, check whether related routines are well organized. If not, refactor them.
- **Refactor when you add a class** Adding a class often brings issues with existing code to the fore. Use this time as an opportunity to refactor other classes that are closely related to the class you’re adding.
- **Refactor when you fix a defect** Use the understanding you gain from fixing a bug to improve other code that might be prone to similar defects.
- **Target error-prone modules** Some modules are more error-prone and brittle than others. Is there a section of code that you and everyone else on your team is afraid of? That’s probably an error-prone module. Although most people’s natural tendency is to avoid these challenging sections of code, targeting these sections for refactoring can be one of the more effective strategies (Jones 2000).

> **Cross-Reference** For more on error-prone code, see "Which Classes Contain the Most Errors?" in Section 22.4.
