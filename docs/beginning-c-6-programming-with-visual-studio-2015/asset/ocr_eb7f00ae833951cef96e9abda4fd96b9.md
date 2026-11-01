in Windows Explorer, or from the command prompt. To do this, open a command prompt window, change the directory to C:\BegVCSharp\Chapter02\ConsoleApplication1\ConsoleApplication1\bin\Debug\, type ConsoleApplication1, and press Enter.

> > **NOTE** In future examples, when you see the instructions “create a new console project” or “execute the code,” you can choose whichever method you want to perform these steps. Unless otherwise stated, all code should be run with debugging enabled. In addition, the terms “start,” “execute,” and “run” are used interchangeably in this book, and discussions following examples always assume that you have exited the application in the example.

Console applications terminate as soon as they finish execution, which can mean that you don’t get a chance to see the results if you run them directly through the IDE. To get around this in the preceding example, the code is told to wait for a key press before terminating, using the following line:

```
Console.ReadKey();
```

You will see this technique used many times in later examples. Now that you’ve created a project, you can take a more detailed look at some of the regions of the development environment.

# The Solution Explorer

By default, the Solution Explorer window is docked in the top-right corner of the screen. As with other windows, you can move it wherever you like, or you can set it to auto-hide by clicking the pin icon. The Solution Explorer window shares space with another useful window called Class View, which you can display using View ⇧ Class View. Figure 2-7 shows both of these windows with all nodes expanded (you can toggle between them by clicking on the tabs at the bottom of the window when the window is docked).

![](bbox=[0.12, 0.78, 0.68, 0.92])

FIGURE 2-7