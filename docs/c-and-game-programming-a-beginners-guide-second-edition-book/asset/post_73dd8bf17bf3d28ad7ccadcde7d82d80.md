
create the effect of true animation, the programmer would have to include some visual changes, a turn to the left, a step to the right, etc. To do this, we'll need to include several alternative images; these will be stored to the `spriteTexture`, which will now be referenced as an array. Here, I've also included a simple try-catch block to monitor the new images. Note that, with Direct3D, a missing file does not halt compilation (see Example 5.82 on the CD-ROM).

## Game 6—Ground Assault

Ground Assault is a combination of all the previous games, as well as several of the classes we just discussed. Once again, we need to lay out a simple plan, develop some characters, weapons, and include a line of movement—this time, I think we'll even develop a few walls.

### Brainstorming

Since the premise of Ground Assault is that the aliens from the last game actually landed, we should start there. First, we'll redesign the aliens to include whole bodies (the better for attacking on foot, my dear). Second, we'll want to redesign our hero so that he's not always looking up. As I stated just a moment ago, we'll also develop some walls, which will be used to stop the missiles and force our characters to work a little for their kills.

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_455_0.png)

### Example 5.83. Brainstorming Ground Assault

- 1. Redesign characters to include bodies, also, use only one character from each color group.
- 2. Redesign the hero so that he's not looking up, and give him the ability to turn in all four directions.
- 3. Redesign the missiles to include all eight directions.
- 4. Add four walls that are repositioned after each new level (set up the first pattern to repeat after you complete the fourth).
- 5. Give the walls a distinct color.
- 6. Give the hero three lives.
- 7. Have him score a set number of points for killing each alien.

### Graphics

We'll also need to think up some colorful designs. In this case, I used extended versions of our alien attacker. We'll once again want to use a smooth change of colors. The coding is also very similar to that in the last game, it uses a simple overriding OnPaint method (as shown in GroundAssault.cs on the CD-ROM).

## Game 7—Rat Racer

For our seventh game, we'll build a simple maze with some obstacles and a goal. The steps are fairly routine: brainstorming, drawing out the characters, and applying the key functions. Here's a mini-version of those steps.

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_456_0.png)

### Example 5.84. Brainstorming Rat Racer.

- 1. Two mice are racing to see who can eat the most cheese.
- 2. There's a maze that they must traverse.
- 3. There will be four cats sitting at each corner of the maze.
- 4. If you move too close to any of those cats, you'll get eaten.
- 5. If one player dies, the other still must eat all the cheese.
- 6. Walking into the walls will kill the mice.
- 7. The cheese will be placed randomly across the board.
- 8. If all the cheese is eaten, the cheese will reset.

### Adding Animation

The mice will have faces and bodies that change slightly as they walk around the board. They will open and close their mouths, curl and uncurl their tails, and rotate their arms. In addition, they should be able to move up, down, left, and right (see Example 5.85).

### Example 5.85. Animations of characters in Rat Racer: a) cats; b) mice; c) cheese

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_457_0.png)

a) Cats.

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_457_1.png)

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_457_2.png)

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_457_3.png)

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_457_4.png)

b) mice

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_458_0.png)

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_458_1.png)

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_458_2.png)

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_458_3.png)

c) cheese

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_458_4.png)

### Troubleshooting

If you've gotten the previous programs to run, but are having trouble with these new ones, then the problem must be in the setup. Try going back over the steps and repeating steps from the earlier games. You might also want to try including all the classes as part of the same file. If the combined file runs correctly, then there must be something wrong with the way you're setting up the secondary files.

### Questions

- 1. Build a simple structure and reference it from the main method. Then, using public fields, rebuild that structure as a class.
- 2. From Question 1, convert that class's public fields into protected fields (build as many secondary methods as you need to get the job done).
- 3. From Question 2, convert those fields into private members. (Hint: You may need to add additional methods.)
- 4. Write a class that allows for both overloaded arithmetic and comparison operators.
- 5. Write a simple public, nested class, and then replace that nested class with an inherited class.

### Assignments

Now that you have a working knowledge of the C# language and a basic grasp of game programming, it's time that you attempt to develop your own games. First, try developing an eighth game that ties into the classes already developed (Note: No new classes should be added). Next, try developing your own set of classes, possibly with two new games, and then one more game where you are again not allowed to alter those classes (in the second test, however, you may opt to build additional inherited classes).

### Conclusion

So, you've mastered the games, and in doing so, have mastered both C# and the concept of object-oriented programming. You might now be wondering, “What is next—where do I go from here?” Or more importantly, “How can I turn these new found skills into a paying profession?” The answer to these questions is, “Through continued study.” You'll want to take a good, hard look at the specialties involved with business and game programming, as well as mathematics, electronics, and engineering. For some, a college degree will be the next step; for others, the MCAD/MCSD will seem like the best road. Ultimately, these choices are left to you.

The book's CD-ROM includes a special selection of text references that may aid you in this journey. I've also included playable and project versions of all the games, as well as the original art, sound clips, and source code to make it possible for you to develop new and/or extended versions. To access the catalog and/or the alternative files, simply search through the CD-ROM using your Windows Explorer and access the appropriate files.

The release versions of the games are also listed in accordance with their chapters (Chapter\Game Title\Bin\Release\Game Title.exe), and can also be accessed through Windows Explorer; however, for best game play, it is recommended that these games be stored on the hard drive.

> Note
>
> If you are using an older version of Windows and would like to access these games without purchasing a .NET compiler, you can do so by downloading the .NET framework which is currently located at http://msdn.microsoft.com/netframework/downloads/default.asp.

Thank you and good luck.

## Appendix A: Keywords/Reserved Identifiers

| abstract | decimal | float | namespace | return | try |
|---|---|---|---|---|---|
| as | default | for | new | sbyte | typeof |
| base | delegate | foreach | null | sealed | uint |
| bool | do | goto | object | short | ulong |
| break | double | if | operator | sizeof | unchecked |
| byte | else | implicit | out | stackalloc | unsafe |
| case | enum | in | override | static | ushort |
| catch | event | int | params | string | using |
| char | explicit | interface | private | struct | virtual |
| checked | extern | internal | protected | switch | void |
| class | false | is | public | this | volatile |
| const | finally | lock | readonly | throw | while |
| continue | fixed | long | ref | true |  |

It is important not to intermix reserved identifiers with programmer-generated references. However, if a situation arises where such a naming conflict cannot be avoided, it is possible to disassociate that identifier from the compiler using the @ symbol (see Example A.1).

### Example A.1.

```csharp
using System;
namespace Appendix_A {
    class Class1 {
        [STAThread]
        static void Main(string[] args) {
            int @true = 325;
            string @while = "Salvatore A. Buono";
            Console.WriteLine(@true);
            Console.WriteLine(@while);
        }
    }
}
```
