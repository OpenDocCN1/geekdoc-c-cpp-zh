
# Scripted utilities

A scripted utility is a MAXScript that has its own custom rollout in the Utilities panel, like the SphereArray example. This type of script is particularly useful when your script has parameters that the user needs to enter, such as the radius in the SphereArray script. Scripted utilities are easy to build using the Visual MAXScript Editor.

# Scripted right-click menus

When you right-click an object in your scene, Max opens a pop-up menu of options for you to choose from, much like a quadmenu. Scripted right-click menus let you append your own menu items to the right-click menu. If you create a script that modifies some property of an object, making the script available through the right-click menu makes it easily accessible.

# Scripted mouse tools

You can use scripted mouse tools to create scripts that handle mouse input in the viewports. These scripts listen for commands from the mouse, such as clicking the mouse buttons and clicking and dragging the cursor. For example, you would use this type of MAXScript if you were making a new primitive object type so that users could create the new objects just like they would a sphere or a box.

# Scripted plug-ins

Scripted plug-ins are by far the most complex type of MAXScript available. They mirror the functionality of non-MAXScript plug-ins (which are written in other programming languages such as C++). You can create scripted plug-ins that make new geometry, create new shapes, control lights, act as modifiers, control texture maps and materials, and even produce special rendering effects.

# Writing Your Own MAXScripts

This section presents the basics of the MAXScript language and shows you how to use the various parts of MAXScript in your own scripts. You can test any of these scripting commands using the MAXScript Listener window.

# Cross-Ref

Much of the discussion that follows will sound familiar if you’ve already read the material on expressions found in Chapter 35, “Animating with the Expression Controller and Wiring Parameters.” Expressions use many of the same constructs as MAXScript.

# Variables and data types

A variable in MAXScript is sort of like a variable in algebra. It represents some other value, and when you mention a variable in an equation, you’re actually talking about the value that the variable holds. You can think of variables in MAXScript as containers that you can put stuff into and take it out of later. Unlike variables in algebra, however, variables in MAXScript can “hold” other things besides numbers, as you’ll soon see.

To put a value into a variable, you use the equal sign. For example, if you type

```
X = 5 * 3
```

in the MAXScript Listener window, Max evaluates the expression on the right side of the equal sign and stores the result in the variable named X. In this case, Max would multiply 5 and 3 and would store the result (15) in X. You can then see what is in X by just typing X in the Listener window and pressing Enter. Max then displays the value stored in X, or 15.

You can name your variables whatever you want, and naming them something that helps you remember what each variable is for is a good idea. For example, if you want a variable that keeps track of how many objects you’re going to manipulate, the name "objCount" would be better than something like "Z."

### Note

Variable names can be just about anything you want, but you must start a variable name with a letter. Also, the variable name can’t have any special characters in it, like spaces, commas, or quotation marks. You can, however, use the underscore character and any normal alphabetic characters.

Variables can also hold strings, which are groups of characters. For example,

```
badDay = "Monday"
```

stores the word "Monday" in the variable badDay. You can attach two strings together using the plus sign, like this:

```
grouchy = "My least favorite day is" + badDay
```

Now the variable grouchy holds the value "My least favorite day is Monday."

Try this:

```
wontWork = 5 + "cheese"
```

Max prints out an error because it’s confused: You’re asking it to add a number to a string. The problem is that 5 and "cheese" are two different data types. Data types are different classes of values that you can store in variables. You can almost always mix values of the same data type, but values of different types usually don’t make sense together.

### Note

To see the data type of a variable, use the classof command. Using the previous example, you could type classof grouchy, and Max would, in turn, print out String.

Another very common data type is Point3, which represents a three-dimensional point. Following are a few examples of using points, with explanatory comments:

```
Pos = [5,3,2]      -- Marks a point at (5,3,2)
Pos.x = 7          -- Change the x coordinate to 7
                   -- Now the point is at (7,3,2)
Pos = Pos + (1,2,5) -- Take the old value for Pos,
                   -- move it by (1,2,5) to (8,5,7)
                   -- and store the new value in Pos
```

In addition to these basic data types, each object in your scene has its own data type. For example, if you use classof on a sphere object, Max prints out Sphere. Data types for scene objects are actually complex data types or structures, which means that they are groups of other data types in a single unit. The pieces of data inside a larger object are called members or properties. Most scene objects have a member called Name, which is of type String. The Name member tells the specific name of that object. Another common property is Position, a Point3 variable that tells the object’s position.

Max has a special built-in variable that represents whatever object is currently selected. This variable is $ (the dollar sign), which is used in the following tutorial.

# Tutorial: Using variables

In this tutorial, you learn more about variables in MAXScript by using them to manipulate an object in your scene.

To use variables to manipulate scene objects, follow these steps:

- 1. Open the Teapot.max file from the Chap 49 directory on the DVD.
  This file has a simple teapot object.

- 2. Right-click on the title for the Left viewport, and choose Views ⇔ Extended ⇔ MAXScript Listener to open the MAXScript Listener window in the Left viewport.

- 3. Select the teapot object, type $, and press Enter.
  Max displays information about the teapot. (Your numbers will probably be different depending on where you placed your teapot.)

- 4. Type the following lines one at a time in the top pane to see the property values stored as part of the teapot object:
  $.position
  $.wirecolor
  $.radius
  $.name
  $.lid

- 5. Now type these lines, one at a time, to set the property values of the teapot object:
  $.lid = false
  $.position.x = -20
  $.segs = 20

Figure 49.13 shows the commands, their results in the MAXScript Listener window, and the resulting teapot object.

# Program flow and comments

In general, when Max begins executing a script, it starts with the first line of the script, processes it, and then moves on to the next line. Execution of the script continues until no more lines are in the script file. (Later, you'll look at some MAXScript keywords that let you change the flow of script execution.)

Max lets you embed comments or notes in your script file to help explain what is happening. To insert a comment, precede it with two hyphens (--). When Max encounters the double hyphen, it skips the comment and everything else on that line and moves to the next line of the script. For example, in this line of MAXScript

```
$Torus01.pos = [0,0,0]  -- Move it back to the origin
```

Max processes the first part of the line (and moves the object to the origin) and then moves on to the next line after it reaches the comment.

Using comments in your MAXScript files is very important because as your scripts start to become complex, figuring out what is happening can get difficult. Also, when you come back a few months later to improve your script, comments will refresh your memory and help keep you from repeating the same mistakes you made the first time around.

### Note

Because Max ignores anything after the double hyphen, you can use comments to temporarily remove MAXScript lines from your script. If something isn't working right, you can comment out the lines that you want Max to skip. Later, when you want to add them back in, you don't have to retype them. You can just remove the comment marks, and your script is back to normal.
