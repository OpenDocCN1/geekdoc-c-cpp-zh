# # Building Game Classes

As with previous games, our next two also rely on a set of classes, their instances, and a host of methods that manipulate data to produce what we see as our cyber creations. These instances and their components were constructed using the knowledge base gathered in this chapter, it is therefore prudent to discuss these techniques here. The first class that we’ll discuss is a key component in all the games; it was used to create the characters, their weapons, and nearly all of the objects that appeared on the screen.

# ## Game Classes—AnimatedImage.cs

The class named AnimatedImage will be used to control our characters, including their appearance, movements, and limitations. Preceding this class we’ll include a set of System references; these are required by several of the methods included in the next few sections. It is always necessary to wrap our classes inside of a clearly marked namespace, in this case the namespace Games. Then, we’ll declare some fields and create our constructors (notice how essential constructor overloading becomes with regard to multiple setups—see AnimatedImage.cs in the Game Classes folder on the CD-ROM).

# ### Example 5.61. AnimatedImage.cs

```
```
/* AnimatedImage.cs: Contains the AnimatedImage class, which is a
* generic class capable of holding and doing animation logic for
* an image. You can sub-class this object to customize its behavior.
*/

using System;
using System.Drawing;

namespace GameClasses {
    public class AnimatedImage {
        // Constants
        public const int DEFAULTSTEP = 3;
        public const int SOUTHWEST = 1;
        public const int SOUTH = 2;
        public const int SOUTHEAST = 3;
        public const int EAST = 4;
        public const int NORTHEAST = 5;
        public const int NORTH = 6;
```
```