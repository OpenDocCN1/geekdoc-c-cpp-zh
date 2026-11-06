![](bbox=[0.153, 0.135, 0.228, 0.208])

C++ programmers use the term *escape-sequence* to refer to any special character in a string that starts with a backslash. This is an outdated bit of vocabulary — maybe not as old as “methinks,” but it does date back to the original C language of the 1970s. Back then, you made special characters appear on console screens by first pressing the Esc key.

# # Let Your Application Run Away

The word *execute* refers to running your application, but you need to compile (or *build*, using the Code::Blocks terminology) the application before you run it. The compilation process transforms your application into an executable file. An *executable file* is a special type of file that contains an application you can run on your computer. When you run your word processor application, you run an executable file containing the word processor application.

![](bbox=[0.153, 0.404, 0.228, 0.476])

After the computer compiles (builds) your application, it performs a step called *linking*. People often refer to these two steps together as simply *compiling*. Indeed, in this book, we often use the term to mean both steps together. If you’re curious about what goes on here, take a look at Appendix A. It has a section devoted to the compiling and linking processes.

Whenever you want to run your application, you first compile it and then you run it. If you make more changes to your application, you must compile it again before running it. Otherwise, the executable file won’t have your changes.

Because you almost always use Build and Run in sequence, the kind people who built Code::Blocks included a special menu item called Build and Run on the Build menu. The computer first compiles your code, and then it immediately runs the application if there are no errors. If there are errors, the compiler doesn’t run the application, and the errors are reported as usual.

We almost always use the Build and Run option rather than click Build and then Run separately. Sometimes, the old-fashioned approach is more efficient: When we compile and run our applications, we use shortcut keys. It takes a bit of extra time to grab the mouse, move the pointer to a menu, and so on. Instead, we press F9 to compile.

Table 2-3 lists keyboard shortcuts for compiling.

| **Table 2-3** | **Keyboard Shortcuts for Compiling and Running** |
|---|---|
| *Action* | *Keyboard Shortcut* |
| Build | Ctrl+F9 |
| Run | Ctrl+F10 |
| Build and run | F9 |