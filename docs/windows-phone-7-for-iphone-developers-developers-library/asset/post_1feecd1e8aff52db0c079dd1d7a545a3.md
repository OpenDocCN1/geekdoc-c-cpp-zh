
![](img/04a00d46bb1059867d95707babd62ee7_295_0.png)

Figure 20.1 Printing custom text upon hitting a breakpoint.

You might notice that after you make the change indicated in Figure 20.1 to a standard breakpoint and debug your application, the “red ball” shape on the left side changes to a diamond, indicating that there is more to this breakpoint than simply stopping execution on that line. As an added trick, I often label all of my “print debug” breakpoints with the same label so that I can find and deactivate them later. Another useful tip: deactivate your breakpoints instead of deleting them. This way you can turn them back on when you need them. This is especially handy for breakpoints like the one mentioned previously that prints valuable information during a debug session.

When I run the application with this breakpoint active on one of my own apps, I see messages like the following show up in my Debug output window, and execution never stops as I click between active Pivot panels:

```
Function: ApocalypseTrainer.MainPage.mainPivot_SelectionChanged(object, System.Windows.Controls.SelectionChangedEventArgs), Selected Index: 1
Function: ApocalypseTrainer.MainPage.mainPivot_SelectionChanged(object, System.Windows.Controls.SelectionChangedEventArgs), Selected Index: 2
Function: ApocalypseTrainer.MainPage.mainPivot_SelectionChanged(object, System.Windows.Controls.SelectionChangedEventArgs), Selected Index: 3
Function: ApocalypseTrainer.MainPage.mainPivot_SelectionChanged(object, System.Windows.Controls.SelectionChangedEventArgs), Selected Index: 0
Function: ApocalypseTrainer.MainPage.mainPivot_SelectionChanged(object, System.Windows.Controls.SelectionChangedEventArgs), Selected Index: 1
```

In Visual Studio 2010, if you click the Debug menu and hover over the Windows option, you should see three additional choices: Breakpoints, Output, and Immediate.

Clicking the Breakpoints option will usually dock the breakpoints window to the bottom of your IDE but, depending on your options, it might show it as a floating window.

This window shows all the breakpoints, their labels, conditions, and hit counts for your solution. Remember when I mentioned that I often use the “labeling” feature to group all my debug-printing breakpoints together. If I use a label like “debugprint,” I can then use this window to search for all breakpoints with that label by typing “debugprint” into the search box and pressing Enter. With those results in the window, I can enable or disable all those breakpoints with a single button-click, and I don’t have to hunt across hundreds of files in dozens of projects to find all my breakpoints.

Before you continue to the next section, I highly recommend you spend some time playing with breakpoints. They are an often overlooked feature of VS2010. Most developers know how to stop execution all the time on a single line of code, but just as many developers forget that there are a host of other things you can do with breakpoints.

## Logging and the Debug Class

You’ve already seen how to use a special type of breakpoint to print out information to the debug log. In this section, I’ll cover a couple of techniques (as well as WP7-specific limitations) for logging other important runtime data as you troubleshoot your app.

If you’ve written any iOS (or Mac) applications, you’re familiar with the NSLog function. This function is used extensively by iOS developers to keep track of important information, events, and data as it flows through the application. They use it to make sure that assumptions about data on which their code operates are correct and to print out useful information while developing an application.

The Windows Phone 7 equivalent of the NSLog function is the Debug.WriteLine method. You use this method in much the same way as you use NSLog—to dump whatever information you feel is important to the debug log.

Windows and web developers who have experience with Visual Studio 2010 might be a little disappointed to notice that the number of methods on the Debug class are limited and that the Trace class is missing entirely. For whatever reason, there is no out-of-the-box method by which you can trace information to a text file in WP7 like there is on desktop or server platforms with VS2010.

It’s really a matter of personal preference whether you pepper your code with Debug.WriteLine statements or whether you use the breakpoint technique I outlined previously. I personally prefer to use the breakpoint technique because it allows me to toggle different types of output without having to delete or comment out code. Additionally, when I’m ready to submit the application for production certification through the Marketplace, I don’t have to worry about tracking down all my Debug.WriteLine statements and removing them. On the other hand, if something about a large number of breakpoints bothers you, you might be more comfortable using Debug.WriteLine instead.

## Using Static Analysis

So, you’ve been diligent and you’ve been creating unit tests to make sure your code does what you expect. You’ve been debugging your code and you’ve uncovered all kinds of nasty little critters, but you’ve also managed to squash all those bugs. You’re sitting back in your chair thinking that you’re ready to upload your masterpiece to the application Marketplace. But wait, there’s more!

There’s another tool in the Windows Phone 7 developer toolbox that can help hone your application code into a finely chiseled blade (a Ginsu, perhaps?). Microsoft has come up with an extensive set of rules, recommendations, and warning signs culled from years of experience and developer feedback. This set of prescriptive guidance has been integrated directly into a static code analysis tool that is built in to Visual Studio 2010. In other words, VS2010 can dig through your code and point out some very common problems and even recommend ways that you might be able to fix them.

For example, the static analysis tool can track the method calls and property accessors in your code and find areas where you might accidentally fall victim to the law of unintended consequences. A very common situation here is when code calls a property accessor and the property accessor then invokes some other function, and that function can be overridden in child classes. This creates a foggy area that allows vast amounts of code to potentially execute as a result of a simple property set that you wrote. A developer unaware of your original intent might be able to come along and override that method and neither of you might immediately notice the consequences of this. Thankfully, the VS2010 static analysis tool is aware of this and thousands of other possible “gotchas.”

Figure 20.2 shows what it looks like after code analysis has been run on a Windows Phone 7 application project. To trigger code analysis, all you need to do is right-click a project and choose Run Code Analysis. This will build the application and then perform an analysis of your compiled code.

![](img/04a00d46bb1059867d95707babd62ee7_297_0.png)

Figure 20.2 Results of code analysis on a sample project.

In Figure 20.2, you can see that I’ve got a couple of spots where the static analysis tool is warning me that I should check a call execution chain for unintended consequences. In one of these cases, I really do want those consequences, and I’m stubborn and my boss is yelling at me, and I need to get home to my Xbox, so I want to suppress that warning instead of looking for a way to refactor my code to avoid the warning.

There are a couple of different ways to suppress these warnings. To start, highlight the warning in the list and right-click it. When you choose the Suppress Message(s) option, you can choose to suppress the message “in source” or in a project suppression file.

If you choose to suppress the message in source, this creates an attribute that sits at the scope of the code block that violated whatever static analysis rule triggered the warning. The next time you run code analysis, this warning message will not appear.

Personally, I feel that littering my source code with attributes that only apply at build time and only during code analysis is ugly. Thankfully, I can choose to suppress the static analysis warnings in a project suppression file. If I choose this option, an attribute will be created in a file called GlobalSuppressions.cs.

### Listing 20.1 GlobalSuppressions.cs

```
// This file is used by Code Analysis to maintain SuppressMessage
// attributes that are applied to this project.
// Project-level suppressions either have no target or are given
// a specific target and scoped to a namespace, type, member, etc.
//
// To add a suppression to this file, right-click the message in the
// Error List, point to "Suppress Message(s)", and click
// "In Project Suppression File".
// You do not need to add suppressions to this file manually.

[assembly: System.Diagnostics.CodeAnalysis.SuppressMessage(
"Microsoft.Usage",
"CA2214:DoNotCallOverridableMethodsInConstructors",
Scope = "member",
Target = "ApocalypseTrainer.ViewModel.FoodItem.#ctor()")]
```

I joke about suppressing the static analysis warnings for trivial reasons, but the truth is that you should spend a little bit of time figuring out why the warning appeared and what problems are associated with that warning before you suppress it. Each one of the code analysis warnings has a unique number (such as CA2214 in the preceding sample). If you aren’t sure why the static analysis tool is warning you, enter that number into your favorite search engine and see whether anything comes up. I have been pleasantly surprised at how much detail I can find online about some of the CA rules and warnings.
