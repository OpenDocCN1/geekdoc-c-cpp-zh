# C# During Its Abstract Period

Most methods — even those built into the C# library — use the ToString() method to display objects. Thus overriding ToString() has the useful effect of displaying the object in its own, unique format, no matter who does the displaying.

Always override ToString().

# C# During Its Abstract Period

The duck is a type of bird, I think. So are the cardinal and the hummingbird, in fact, every bird out there is a subtype of bird. The flip side of argument that there is no bird that isn't some subtype of Bird. That statement doesn't sound profound, but in a way, it is. The software equivalent of statement is that all bird objects are instances of subclass of Bird — there's never an instance of class Bird. What's a bird? It's like a robin or a grackle or another specific species.

Different types of birds share many properties (otherwise, they wouldn't be birds), yet no two types share every property. If they did, they wouldn't be different types. To pick a particularly large example, not all birds Fly() the same way. Ducks the cardinal's style is similar but not identical. (Don't get me started about emus and ostriches or the rubber duck in your tub.)

But if not birds fly the same way and there's no such thing as a Bird, what the heck is Bird.Fly()? The subject of the following sections, is what it is.

# Class factoring

People generate taxonomies of objects by factoring out commonalities. To see how factoring works, consider the two classes HighSchool and University, shown in Figure 7-1. This figure uses the Unified Modeling Language (UML), a graphical language that describes a class along with the relationship of that class to others. UML has become universally popular with programmers and is worth learning (to a reasonable extent) in its right.

Figure 7-1: A UML description of High School and University classes.

| High School | | University |
| --- | --- | --- | --- |
| - numStudents | Student | - numStudents | Student |
| + Enroll () | | + avgSAT | |
| | | + Enroll () | |
| | | + GetGrant () | |