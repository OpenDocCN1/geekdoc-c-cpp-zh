
## MORE THAN EDITING...

Basic text editing in Visual Studio complies with Windows standards. You can double-click to select a word, ctrl-click to extend the selection, and cut, copy or paste selections just the way you're used to. But the Visual Studio Code Editor also includes a seemingly magical tool called Intellisense that turns it from a stenographer into a personal assistant.

> Intellisense will even create standard code and objects for you.

> What else does the new gizmo come in?

> Intellisense shows you what an object can do as you type, so you don't need to memorize a lot of detailed syntax.

> Send this guy a "Don't call us, we'll call you" letter.

> What are the specifications for this new gizmo?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_94_0.png)

## LIST MEMBERS

The Intellisense capability that you'll probably use most often is the LIST MEMBERS function that displays a list of valid "things" that can be inserted where you're typing. You saw the list members function when you built your first application in Chapter 2.

As soon as you type a single character, the List Members box will open. Visual Studio is pretty smart about knowing what you can do, and it won't list things that don't apply (but it's not very smart about what makes sense).

To insert the selected item, press the Tab key or type the character after the item. In this case, that would be the "(" character, and you know that because of the definition displayed in the little help box on the far left.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_95_0.png)

When you select an item in the box, Visual Studio shows you the definition of the item, a short description, and, if the item is a method something an object knows how to do any exceptions the method can throw in a little help box.

To highlight an item in the List Members box, you can keep typing characters to limit the list, or use the up and down arrow keys.

The box lists everything that contains the letters you type, not just the ones that begin with what you type. Typing "n", for example, would display both "NewItem" and "EditNew", assuming they were available.

An EXCEPTION is the way an object lets the rest of the program know something is wrong. We'll look at exceptions and what to do about them in Chapter 7.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_95_1.png)

## PARAMETER INFORMATION

METHODS are things that objects can do. (We'll look at exactly what "object" and "method" mean in detail in Chapter 8.) Some methods take PARAMETERS, which are bits of information that you pass to the method to control exactly how it does whatever it does. In the bad old days before Intellisense, programmers spent a lot of time trying to remember exactly what parameters a method took, and in what order. The Intellisense Parameter Info box eliminates all that by showing you exactly what your options are.

As soon as you type the opening paren of a method call, Intellisense displays the Parameter Info box that shows you the method definition, a description of the method, and of the first parameter.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_96_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_96_1.png)

As you type each parameter, Intellisense updates the display to show the description of the next one.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_96_2.png)

List Members works right alongside Parameter Info, so sometimes the screen can get a bit crowded! Mostly it's helpful, but if all the windows get in your way, you can always make them go away by pressing Esc.

## ROAD MAPS

Several editing functions help you keep track of where you are and what you've done. Using them is pretty intuitive, but here's a quick rundown:

### CODE OUTLINING

Click on the '+' and '-' characters in the left margin to collapse and expand units of code.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_97_0.png)

### QUICK INFO

Hover the mouse over any identifier, and Intellisense will display its definition and a description.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_97_1.png)

### REFERENCE HIGHLIGHTING

Select any symbol in the editor by double-clicking it, and it will highlight all the references to that symbol in the code.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_97_2.png)

## REFACTORING

REFACTORING is a fancy programming term for “cleaning up”. Visual Studio provides some very sophisticated support for refactoring, saving you hours of tedious work and making it far more likely that you’ll keep your code clean and tight. Unfortunately, most of that support won’t make sense to you yet, so we’ll talk about it later. But one refactoring function is immediately useful: you can tell Visual Studio that you want to re-name something, and it will find and update every place you’ve referred to it. Let’s try it in the MainWindow code. (If the code window isn’t open, you can double-click it in the Solution Explorer and then press F7 to display the code window.)

In the button click event that you created, right-click on the name of the window, newWin, and choose Refactor and then Rename from the context menu. Notice that the shortcut key for Rename is F2, the standard Windows shortcut for renaming something.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_98_0.png)

When you select Rename from the context menu (or press F2), Visual Studio will display the Rename dialog. Type “myNewWin” in the New name text box, leave the other choices as they are, and click OK.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_98_1.png)

Because we left “Preview reference changes” checked in the Rename dialog, Visual Studio will display the Preview Changes dialog after you click OK. In such a simple example, you only need to confirm that you’re changing what you thought you were changing, so if you are, click Apply.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_99_0.png)

And, like magic, the window is renamed. Well, it might not seem like magic yet, just a complicated form of search and replace. But here’s the magical part: Visual Studio will change the name in every file in the project. Try doing that with search and replace!

```
private void button1_Click(object sender, RoutedEventArgs e)
{
    Window myNewWin = new Window1();
    myNewWin.Show();
}
```

### TAKE A BREAK

You've almost finished this chapter, so take a short break before you come back for the final Review.

## REVIEW

Name at least one way to add a Project to a Solution:

Name at least two ways to add a File to a Project:

Where would you assign an application icon?

What does this widget do?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_100_0.png)

On a new, blank line inside the Button1_click event handler, type an “a” to trigger Intellisense. What’s the description of the Array object?

How many versions of the Array.BinarySearch() method are there?

Hover the mouse over one of the instances of the Window identifier. (There are two in your source file.) What’s the description of the Window?

## Congratulations! You've finished the chapter. Take a minute to think about what you've accomplished before you move on to the next one...

### List three things you learned in this chapter:

- 1
- 2
- 3

Why do you think you need to know these things in order to be a C# programmer?

Is there anything in this chapter that you think you need to understand in more detail? If so, what are you going to do about that?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_102_0.png)

## TEST AND DEPLOY

The little applications we've been building so far have been simple throw-aways, intended only to demonstrate the use of the Visual Studio IDE, and you've been given pretty detailed instructions for creating them. But it won't be long before you're creating applications on your own, and if you get all your code right on the first try, you'll be the first to do so. So we'll start this chapter off by looking at the support that

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_103_0.png)

Visual Studio provides for finding and fixing errors, and then we'll look at the tools for deploying your applications once they're finished.

> MAKE A NOTE
>
> The conventional wisdom in the development community is that there are always at least three bugs in every program: the one you know about, the one you don't know about, and the one you're going to create when you fix the one you know about...
