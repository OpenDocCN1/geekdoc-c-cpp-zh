
Logic errors are the most challenging errors to find and to fix. And worst of all, logic errors often go unnoticed. In March 1985, I got a monthly home heating bill for $1,328,932.21. Clearly, some computer had printed the incorrect amount. When I called the gas company to complain about it, the telephone service representative said, "Don't be upset. Pay only half that amount."

**Compile-time warnings:** A warning isn't as severe as an error message. So, when Eclipse notices something suspicious in your program, the editor displays a jagged yellow underline, a tiny yellow icon containing an exclamation point, and a few other not-so-intrusive clues.

For example, in the figure below I add something about `amount = 10` to the code from Listing 3-1. (It's that bit on line 8.) The problem is, I never make use of the `amount` or of the number 10 anywhere in my program. With its faint yellow markings, Eclipse effectively tells me "Your `amount = 10` code isn't bad enough to be a show-stopper. Eclipse can still manage to run your program. But are you sure you want `amount = 10` (the stuff that seems to serve no purpose) in your program?"

![](img/6d9dcff12e52b997f3ad31445b712549_83_0.png)

Imagine being told to "turn when you reach the intersection." The direction may be just fine. But if you're suspicious, you ask, "Which way should I turn? Left or right?"

When you're sure you know what you're doing, you can ignore warnings and worry about them at some later time. But a warning can be an indicator that something more serious is wrong with your code. So my sweeping recommendation is this: Pay attention to warnings. But, if you can't figure out why you're getting a particular warning, don't let the warning prevent you from moving forward.

## What's All That Stuff in Eclipse's Window?

Believe it or not, an editor once rejected one of my book proposals. In the margins, the editor scribbled "This is not a word" next to things like "can't," "it's," and "I've." To this day, I still do not know what this editor did not like about contractions. My own opinion is that language always needs to expand. Where would we be without new words — words like *dotcom*, *infomercial*, and *vaporware*?

![](img/6d9dcff12e52b997f3ad31445b712549_86_0.png)

When you use a view to change something, the change takes place immediately. For example, when you choose Delete in the Package Explorer's context menu, whatever item you've selected is deleted immediately. In a way, this behavior is nothing new. The same kind of thing happens when you recycle a file using Windows Explorer or trash a file using the Macintosh Finder.

> Editor: A part of the Eclipse workbench that displays information for you to modify. A typical editor displays information in the form of text. This text can be the contents of a file. For example, an editor in Figure 3-10 displays the contents of the `MyFirstJavaClass.java` file.

![](img/6d9dcff12e52b997f3ad31445b712549_86_1.png)

When you use an editor to change something, the change doesn't take place immediately. For example, look at the editor in Figure 3-10. This editor displays the contents of the `MyFirstJavaClass.java` file. You can type all kinds of things in the editor. Nothing happens to `MyFirstJavaClass.java` until you choose File→Save from Eclipse's menu bar. Of course, this behavior is nothing new. The same kind of thing happens when you work in Microsoft Word or in any other word-processing program.

![](img/6d9dcff12e52b997f3ad31445b712549_86_2.png)

Like other authors, I occasionally become lazy and use the word "view" when I really mean "view or editor." When you catch me doing this, just shake your head and move onward. When I'm being very careful, I use the official Eclipse terminology. I refer to views and editors as parts of the Eclipse workbench. Unfortunately, this "parts" terminology doesn't stick in peoples' minds very well.

An area of the Eclipse workbench might contain several views or several editors. Most Eclipse users get along fine without giving this "several views" business a second thought (or even a first thought). But if you care about the terminology surrounding tabs and active views, here's the scoop:

> Tab: Something that's impossible to describe except by calling it a "tab." That which we call a tab by any other name would move us as well from one view to another or from one editor to another. The important thing is, views can be stacked on top of one another. Eclipse displays stacked views as though they're pages in a tabbed notebook. For example, Figure 3-14 displays one area of the Eclipse workbench. The area contains five views (the Problems view, the Javadoc view, the Declaration view, the Search view, and the Console view). Each view has its own tab.

A bunch of stacked views is called a tab group. To bring a view in the stack to the forefront, you click that view's tab.

And, by the way, all this stuff about tabs and views holds true for tabs and editors. The only interesting thing is the way Eclipse uses the word "editor." In Eclipse, each tabbed page of the editor area is an individual editor. For example, the Editor area in Figure 3-16 contains three editors (not three tabs belonging to a single editor).

Figure 3-16:
The editor area contains three editors.

![](img/6d9dcff12e52b997f3ad31445b712549_87_0.png)

✔ **Active view or active editor:** In a tab group, the view or editor that's in front.

In Figure 3-16, the MyFirstJavaClass.java editor is the active editor.
The Mortgage.java and ThingsILike.java editors are inactive.

## What's inside a view or an editor?

The next several terms deal with individual views, individual editors, and individual areas.

✔ **Toolbar:** The bar of buttons (and other little things) at the top of a view (see Figure 3-17).

Figure 3-17:
The Package Explorer view's toolbar.

![](img/6d9dcff12e52b997f3ad31445b712549_87_1.png)

✔ **Menu button:** A downward-pointing arrow in the toolbar. When you click the menu button, a drop-down list of actions appears (see Figure 3-18).
Which actions you see in the list varies from one view to another.

![](img/6d9dcff12e52b997f3ad31445b712549_88_0.png)

**Figure 3-18:** Clicking the Package Explorer view’s menu button.

**Close button:** A button that gets rid of a particular view or editor (see Figure 3-19).

![](img/6d9dcff12e52b997f3ad31445b712549_88_1.png)

**Figure 3-19:** An editor’s Close button

**Chevron:** A double arrow indicating that other tabs should appear in a particular area (but that the area isn’t wide enough). The chevron in Figure 3-20 has a little number 2 beside it. The 2 tells you that, in addition to the two visible tabs, two tabs are invisible. Clicking the chevron brings up a hover tip containing the labels of all the tabs (see Figure 3-20).

![](img/6d9dcff12e52b997f3ad31445b712549_88_2.png)

**Figure 3-20:** The chevron indicates that two editors are hidden.

**Marker bar:** The vertical ruler on the left edge of the editor area. Eclipse displays tiny alert icons, called *markers*, inside the marker bar. (For example, refer to Figure 3-12.)

## Returning to the big picture

The next two terms deal with Eclipse's overall look and feel.

**Layout:** An arrangement of certain views. The layout in Figure 3-3 has seven views, of which four are easily visible:
- At the far left, you see the Package Explorer view.
- On the far right, you have the Task List view and the Outline view.
- Near the bottom, you get the Problems, Javadoc, Declaration, and Console views.

Along with all these views, the layout contains a single editor area. Any and all open editors appear inside this editor area.

**Perspective:** A very useful layout. If a particular layout is really useful, someone gives that layout a name. And if a layout has a name, you can use the layout whenever you want. For example, the workbench of Figure 3-3 displays Eclipse's *Java perspective*. By default, the Java perspective contains six views in an arrangement very much like the arrangement shown in Figure 3-3.

![](img/6d9dcff12e52b997f3ad31445b712549_89_0.png)

The Console view appears in Figure 3-3, but the Console view doesn't always appear as part of the Java perspective. Normally, the Console view appears automatically when you run a text-based Java program. If you want to force the Console view to appear, choose Window⇒Show View⇒Other. In the resulting Show View dialog box, expand the General branch. Finally, within that General branch, double-click the Console item.

Along with all these views, the Java perspective contains an editor area. (Sure, the editor area has several tabs, but the number of tabs has nothing to do with the Java perspective.)

You can switch among perspectives by choosing Window⇒Open Perspective in Eclipse's main menu bar. This book focuses almost exclusively on Eclipse's Java perspective. But if you like poking around, visit some of the other perspectives to get a glimpse of Eclipse's power and versatility.
