These color differences are just one way in which Xcode lets you know when you (may) have done something wrong.

# ## How do I run my program?

When the contents of your main.c file match what you see above, it's time to run your program and see what it does. This is a two-step process. Xcode builds your program and then runs it. When building your program, Xcode prepares your code to run. This includes checking for syntax and other kinds of errors.

Look again at the lefthand area of the Xcode window. This area is called the navigator area. At the top of the navigator area is a series of buttons. You are currently viewing the project navigator, which shows you the files in your project. The project navigator’s icon is 📋.

Now find and click the 📖 button to reveal the log navigator. The log is Xcode’s way of communicating with you when it is building and running your program.

You can also use the log for your own purposes. For instance, the line in your code that reads

```
```C
printf("It was the best of times.\n");
```
```

is an instruction to display the words “It was the best of times.” in the log.

Since you haven’t built and run your program yet, there isn’t anything in the log navigator. Let’s fix that. In the upper lefthand corner of the project window, find the button that looks suspiciously like the Play button in iTunes or on a DVD player. If you leave your cursor over it, you’ll see a tool tip that says Build and then run the current scheme. That is Xcode-speak for “Press this button, and I will build and run your program.”

If all goes well, you’ll be rewarded with the following:

![](bbox=[0.42, 0.54, 0.58, 0.62])

If not, you’ll get this:

![](bbox=[0.42, 0.67, 0.58, 0.75])

What do you do then? Carefully compare your code with the code in the book. Look for typos and missing semicolons. Xcode will highlight the lines it thinks are problematic. After you find the problem, click the Run button again. Repeat until you have a successful build.

(Don’t get disheartened when you have failed builds with this code or with any code you write in the future. Making and fixing mistakes helps you understand what you’re doing. In fact, it’s actually better than lucking out and getting it right the first time.)