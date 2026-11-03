+   » Inserting code to help you debug
+   » Configuring a project for debugging
+   » Using Code::Blocks' GNU debugger
+   » Stepping through a program
+   » Checking the values of variables
+   » Writing better error messages

# Chapter 25

# Out, Bugs!

Everyone writes buggy code. Not intentionally, of course. Even the best programmers get lazy or sloppy and do silly things. Stray semicolons, misplaced commas, and missing curly brackets happen to all programmers. Fortunately, the compiler catches a lot of this crummy code. Fix the source code and recompile to deal with those annoying, typical bugs.

For deeper problems, flaws in logic, or maybe code boo-boos that aren’t easy to find, it helps to have a little assistance. That assistance comes in the form of debugging your code, which you can do manually or with the help of a debugger. The goal is to see what’s gone wrong.

# Simple Tricks to Resolve Problems

When I can’t figure out what’s going on with a program and I’m too lazy to run it through a debugger, I use the printf() and puts() functions as my debugging friends. These tools can output helpful messages and values, assisting me in determining what’s buggy with the code.