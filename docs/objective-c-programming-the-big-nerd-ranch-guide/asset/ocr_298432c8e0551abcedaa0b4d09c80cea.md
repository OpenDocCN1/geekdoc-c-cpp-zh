# return

![](bbox=[0.06, 0.11, 0.93, 0.45])

You can see this frame’s variables and their values on the bottom left of the window. To the right, you can also see the output in an area called the *console*. (If you don’t see the console, find the `⊡ ⊡ ⊡ ⊡` buttons at the right of the screen towards the bottom half. Click the middle button to reveal the console.) In the console, you can see the effect of your breakpoint: the program stopped before reaching the line that ends the song.

Now we need to remove the breakpoint so that the program will run normally. You can simply drag the blue indicator off the gutter. Or click the `■` icon at the top of the navigator area to reveal the *breakpoint navigator* and see all the breakpoints in a project. From there, you can select your breakpoint and delete it.

To resume execution of your program, click the `▶` button on the debugger bar between the editor and the variables view.

We just took a quick look at the debugger here to demonstrate how frames work. However, using the debugger to set breakpoints and browse the frames in a program’s stack will be helpful when your program is not doing what you expect and you need to look at what is really happening.

# return

Many functions return a value when they complete execution. You know what type of data a function will return by the type that precedes the function name. (If a function doesn’t return anything, its return type is *void*.)

Create a new C Command Line Tool named *Degrees*. In *main.c*, add a function before *main()* that converts a temperature from Celsius to Fahrenheit. Then update *main()* to call the new function.