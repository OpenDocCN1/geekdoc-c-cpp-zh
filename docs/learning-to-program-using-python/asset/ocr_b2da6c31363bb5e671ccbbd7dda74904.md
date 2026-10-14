suites include the GUI libraries required for widget layout.

# ## 20.3 Before You Start

For purposes of this book, I will be talking about wxPython. Though it requires you to download additional software (unlike Tkinter which is included with Python), it has more widgets available to you (making it more versatile) and it allows you to use graphical layout tools, like **wxGlade**, to design the GUI. Otherwise you have to manually place each item in the code, run the program to see how it looks, and go back into your code to make changes. Graphical layout tools let you place widgets wherever you want; when done, you “run” the program which creates the source code template that auto-populates all the widgets. Then you only have to write the underlying logic that make your program work.

Before you start creating a GUI with wxPython, you need to know how to program in Python. This may seem pretty obvious but some people may expect wxPython is self-contained; no additional knowledge required. If you don’t already have Python installed on your computer, you will have to download and install it from the Python web site; this is most common for Windows users. Linux and Mac users already have Python installed.

Additionally, you should have made a few command-line programs in Python so you know how to handle user input and terminal output. My personal suggestion for learning wxPython is to take a command-line program and turn it into a graphical program. This way, you already know how the program works and what the necessary input and expected output should be. All you need to do is create the graphical elements.

I will make a plug for my preference of Python development environments: **SPE**. SPE (Stani’s Python Editor) is an integrated development environment that provides code completion (reduces typing), integrated Python shell (for testing bits of code before you put them into your program), Python calltips (displays expected arguments for the method/function), and various helper tools like notes and todo lists.

Additionally, SPE includes wxPython, which is nice because it was