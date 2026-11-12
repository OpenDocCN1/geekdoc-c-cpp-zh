
Tutorials we will use the default UniSciTE and Unitron; although give some of those other editors a look—they do some great things.

When scripts are created or edited in the editor, they are just text. When the script is saved (back into the Assets folder), Unity will take a look at the text and attempt to compile the script—this means it checks to see if it understands the script. If there are problems, they will show up in the Console and the game will not run until the errors (mostly syntax) have been corrected.

## Console

The Console is actually built in Unity, but is not (by default) shown (although the last line of the Console is visible at the bottom left corner of the interface). It’s accessible via Window>Console. The Console can provide some important information. First, if there are errors in a script, the error will be listed in the Console. The Console will even attempt to let you know which line of which script has the problem. None of the errors can be corrected in the Console, but after fixing the problems, the Console will let you know all’s well by not complaining.

Additionally, the Console can be used to report what’s happening in a script. Scripts can include commands that print values, or list what’s called a Debug.Log that can help track where a script was fired in a game, or what Unity thinks the values of a particular variable are. Being able to see the Console while creating scripts is valuable. So it is visible (Window>Console), and docked within the interface. To dock it, just drag the Console tab to where you wish the Console to reside within the Unity interface.

## What Is a Script?

A script contains commands (statements), organized in blocks and functions, as described next.

## Commands and Statements

At its core, scripts are collections of instructions or **commands** (sometimes also called **statements**). In JavaScript, each command ends with a semicolon. Without a semicolon, Unity will throw an error and require you to go back and add that bit of punctuation before it will even bother reading the statement. An example of a JavaScript command can be as simple as:

```
height = 6;
```

## Blocks

A collection of commands are called **blocks** of code. JavaScript recognizes a block of commands by { and }. It’s important that for every single { there is a }. Again, without this piece of punctuation, Unity won’t bother trying to listen to what you’re saying. See the functions example next for how this works.

## Functions

Commands can be just floating around within a script, but generally, blocks of commands are grouped within a **function**. Grouping commands within a function allows for control over when a collection of commands are actually called on. For instance, if we're pulling a power switch, we only want the animation to play when the character clicks the power switch on; by grouping the collection of commands that do this into a function, we can tie that function to a player's action (like clicking an object).

Any script may contain multiple functions. Some functions are just named by you, the scripter, but there are also some predefined functions in Unity that dictate how a block of code will be carried out, or more importantly, when. These include things like function Update(), which means, “do these instructions every frame of the game,” and function OnMouseDown(), which means, “do these instructions when the player clicks on the object this script is attached to.” Much more on these later.

The key to writing functions is to remember all the appropriate punctuation hints. The format works like this:

```
    function TurnSoundOff()
    {
        audio.enabled = false;
    }
```

We tell Unity we're building a function named TurnSoundOff with function TurnSoundOff and tell it there are no particular parameters for the function with the empty (). Then Unity knows we're starting the block of commands for this function by the {. Then, the command audio.enabled = false; is included and ended with a semicolon. Finally, we tell Unity we're done with this function by ending it with a }.

Capitalization matters. “Function” is not the same as “function.” When defining a function, always use lowercase function. Generally, the name of the function is capitalized. The organization of this example block of code is mostly for readability. The closing } is at the same indentation as the function (so it's easy to see that the function has been closed). However, technically, it could also look like this:

```
    function TurnSoundOff()
        { audio.enabled = false; }
```

which is really tough to read, or like this:

```
    function TurnSoundOff()
    {
        audio.enabled = false;
    }
```

which is easier still to see how the function is created, but can make the code very long and difficult to read in the book. Usually, the way code is formatted is with the fairly standard:

```
    function TurnSoundOff()
    {
        audio.enabled = false;
    }
```

## Variables

Variables are most often described as containers or named locations of information. Variables can contain numbers (**integers**—whole numbers with no decimal, or **float**—number with decimals), on/off switches (**Booleans**), collections of text (**strings**), and XYZ values (**Vector3**) among others. The way scripts work is by declaring the variables that will be used by the script at the beginning of the script (although they can be declared in other places along the way as well). Then, the functions that know of these variables and more importantly of the value that they contain. These can be defined, accessed, or changed in the blocks of code that follows.

Variables are defined with a declaration statement with the `var` label and should start with lowercase. They can include letters and numbers but shouldn't start with a number. Lastly, it's important that a variable not use the name of other reserved terms that Unity uses for other purposes (so no naming a variable “boolean,” for example, since that is used to define a variable type). So, for instance, a variable declaration and access could look like this:

```
var litScene : GameObject;

function TurnLightsOff () {
    litScene.active = false;
}
```

So what's happening there: the script is starting off by declaring the variable litScene (notice it's all one word with lowercase to start and uppercase to define each new word) and we are assigning a type with the `:` GameObject (this could also be Boolean, String, int, or float). Then, in the function TurnLightsOff, we are deactivating this GameObject (which could be any object in Unity) that we've given the name of litScene.

Of course, this script is pretty ineffective right now since we've defined a function but have not told Unity when to “fire” it. It has the instructions, but doesn't know when to use them. We would use other functions like OnMouseDown to trigger that.

## Dot Syntax

This is a very useful mechanism within Unity's JavaScript. Basically it is a way of drilling down through objects to components and then to individual attributes of components. It's a way of accessing information in a hierarchical manner from biggest or most general to smallest or most specific. So for instance if we wanted to set the rotation value of a GameObject that we have defined (with a variable that we've named in the script as enemyTank) we could do it like this:

```
enemyTank.transform.rotation.y = 60;
```

It starts with the GameObject enemyTank, then goes to the transform component, then drills down to the rotation part of that component and then the Y value and enters 60 for its value. Note that enemyTank is a name known only to the script; the name of the object in the hierarchy could be something entirely different. Later, we'll look at how to let the script know that enemyTank is actually the object that we named MyAwesomeTank in Maya. Also later we will look at how this can be used to define variables in other scripts, and even other scripts attached to other GameObjects. When any script can talk to any other script, very sophisticated things can happen.

## Getting to It

That of course isn't everything about scripting. There's loads and loads of powerful functionality there (if-then statements, counting, lerping, etc.), but much of this is best understood in practice rather than endless descriptions of what code is. In the tutorials of this chapter, we will be writing some scripts using the basics described here, and then talk about what we've done. Along the way new ideas will be presented, so be sure to read the Why? sections.

To get going on scripting, we're first going to build a GUI that we can use the scripting mechanism on.

## Tutorial 12.1: Graphical User Interfaces

Graphical User Interfaces (GUI—often pronounced "gooey") are basically the way the user interacts with the computer or program, and usually in ways besides entering text (like through a command line). Computer and web users are very familiar with GUI today, and in fact, most users would be lost without it.

GUI in games are important parts of the gamer's experience. At its most basic level, a GUI will help a player know how to start playing the game after he's been given instructions. In games, GUI has also come to include screen hints or other information that helps the player know what to do and when to do it. The most elegant games provide this guidance in much more intuitive ways, but we will look at some straightforward (but clumsy) methods of providing guidance in the game for the player.

To start with, though, we will use our opening scene as a vehicle to provide a bit of background on the character as well as define the goals of the game. To do this we will make use of Unity's GUITexture mechanism.

### GUITexture

The name of GUITexture gives us some hints as to what sorts of assets it likes to work with—textures. Because it is a texture, it means that Unity will be using an image that it draws on the screen. For this opening GUI (Figure 12.1), we will be using several images—a logo, three buttons (mission, bio, begin), two data panels (one to show the mission and another for Aegis's bio info), and finally a Loading plate.
