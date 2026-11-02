
## DEBUGGING YOUR APPLICATIONS

Debugging your iPhone applications is an essential part of your development journey. Xcode includes debugger utilities that help you trace and examine your code as you execute your application. The following sections show some of the tips and tricks that you can employ when developing your iPhone applications.

### Error

When you try to run your application, Xcode first tries to build the project before it can deploy the application onto the real device or Simulator. Any syntax errors that Xcode detects are immediately highlighted in red. Figure B-10 shows Xcode highlighting a syntax error. The error with the code block is the missing brace symbol (}) for the [[UIAlertView alloc] statement:

```objc
UIAlertView *alert = [[UIAlertView alloc]
                 initwithTitle:@"Hello World"
                 message:@"Hello, My World"
                 delegate:self
                 cancelButtonTitle:@"OK"
                 otherButtonTitles:nil];
[alert show];
[alert release];
}
[super viewDidLoad];
```

![](img/aab2d775c46f70cd606f2e58e2521324_460_0.png)

Can you spot the error? Syntactically, the preceding statements have no problem. However, one of the parameters appears with the wrong capitalization. It turns out that initwithTitle: must be spelled as initWithTitle:. When you compile the program, Xcode will not flag the preceding code as an error, instead, it will issue you with a warning message displayed in yellow (see Figure B-12).

![](img/aab2d775c46f70cd606f2e58e2521324_462_0.png)

FIGURE B-12

When you see a warning message in Xcode, pay special attention to it and check that the method name is spelled correctly, including the capitalization. Failing to do so may result in a runtime exception. Figure B-13 shows the runtime exception message that Xcode displays when a runtime exception occurs.

![](img/aab2d775c46f70cd606f2e58e2521324_462_1.png)

FIGURE B-13

> **NOTE** You can toggle the state of a breakpoint by clicking it to enable or disable it. Breakpoints displayed in dark blue are enabled; those displayed in light blue are disabled.

After you have set breakpoints in your application, you need to press Command-Y to debug your application so that your breakpoints will be stopped when they are reached.

> **NOTE** Pressing Command-R to run the application will not cause the breakpoints to be stopped.

When the application reaches the breakpoint you have set, Xcode displays the current line of execution with a red arrow (see Figure B-16).

![](img/aab2d775c46f70cd606f2e58e2521324_464_0.png)

FIGURE B-16

At this juncture, you can do several things:

- Step Into (Shift-Command-I) — Step into the statements in a function/method.
- Step Over (Shift-Command-O) — Execute all the statements in a function /method and continue to the next statement.
- Step Out (Shift-Command-T) — Finish executing all the statements in a function or method and continue to the next statement after the function call.
- If you want to resume the execution of your application, press Option-Command-P.
- You can also examine the values of variables and objects by clicking the Show Debugger button (see Figure B-17). You can also move your mouse over the objects and variables you are interested in to view their values.

![](img/aab2d775c46f70cd606f2e58e2521324_465_0.png)

FIGURE B-17

### Using NSLog

In addition to setting breakpoints to trace the flow of your application, you can use the `NSLog()` method to print debugging messages to the Debugger Console window. The following `NSLog()` statement prints a message to the Debugger Console window when the application changes orientation:

```objc
- (void)willRotateToInterfaceOrientation:
    (UIInterfaceOrientation) toInterfaceOrientation
    duration: (NSTimeInterval) duration {

    NSLog(@"In the willRotateToInterfaceOrientation: event handler");

    UIInterfaceOrientation destOrientation = toInterfaceOrientation;
    if (destOrientation == UIInterfaceOrientationPortrait)
    {
        btn.frame = CGRectMake(20,20,280,37);
    }
    else
    {
        btn.frame = CGRectMake(180,243,280,37);
    }
}
```

Figure B-18 shows the output in the Debugger Console window (press Shift-Command-R to display it).

![](img/aab2d775c46f70cd606f2e58e2521324_466_0.png)

FIGURE B-18

### Documentations

During the course of your development, you often need to check on the various methods, classes, and objects used in the iPhone SDK. The best way to check them out is to refer to the documentation. Xcode allows you to quickly and easily browse the definitions of classes, properties, and methods through the use of the Option key. To view the help documentation of an item, simply press the Option key. The cursor changes to a cross-hair. Double-click the item you want to check out, and the Developer Documentation window appears (see Figure B-19).

![](img/aab2d775c46f70cd606f2e58e2521324_467_0.png)

FIGURE B-19

### Research Assistant

One very useful tool in the Documentation is the Research Assistant (Help ⇧ Show Research Assistant). The Research Assistant is a window that displays context-sensitive help as you work on your code in Xcode. When you position your cursor on a particular keyword/statement, the Research Assistant will display the following information about the current keyword/statement (see also Figure B-20):

- Declaration
- Abstract
- Availability
- Related API
- Related Documents
- Sample Code

![](img/aab2d775c46f70cd606f2e58e2521324_468_0.png)

FIGURE B-20

### SUMMARY

In this appendix, you had a quick overview of how to use Xcode to develop your iPhone applications. You saw how to use the Debugger Console window to view outputs generated by Xcode while your application is running, as well as how to set breakpoints in your application so that you can step through your code.

## C Getting Around in Interface Builder

Interface Builder is one of the tools shipped with the iPhone SDK. It is a visual design tool that you can use to build the user interface of your iPhone applications. Although not strictly required for the development of your iPhone applications, Interface Builder plays an integral role in your journey of learning about iPhone application development. This appendix covers some of the important features of Interface Builder.

### .XIB WINDOW

The most direct way to launch Interface Builder is to double-click any of the .xib files in your Xcode project. For example, if you have created a View-based Application project, there would be two .xib files in the Resources folder of Xcode. Double-clicking any one of them launches Interface Builder.

When Interface Builder is launched, the first window that you see has the same name as your .xib file (see Figure C-1).

![](img/aab2d775c46f70cd606f2e58e2521324_470_0.png)

FIGURE C-1

Within this window are several items, and depending on what you double-clicked, you should see some of the following items, such as:

- File's Owner
- First Responder
- View, Table View, Window, and so on
- Some View Controllers and delegates

By default, the .xib window is displayed in icon mode. But you can also switch to list mode, where you can view some of the items in more detail. For example, Figure C-2 shows that when viewed in list mode, the View item displays a hierarchy of views contained within it.

![](img/aab2d775c46f70cd606f2e58e2521324_471_0.png)

FIGURE C-2

### DESIGNING THE VIEW

To design the user interface of your application, you typically double-click the View (or Table View or other) item on the .xib window to visually display the window so that you can drag and drop views onto your View window.

To populate your View window with views, you drag and drop objects listed in the Library window (see the Library section for more information on the Library window). Figure C-3 shows a Label view being dropped onto the View window.
