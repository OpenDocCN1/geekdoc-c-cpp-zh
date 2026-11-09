# How it works

The program learns about the important events by reading information from a text file—this is called “file input”. The text file contains the name and date of each event. The code calculates the number of days from today until each event using Python’s `datetime` module. It displays the results in a window created by Python’s `Tkinter` module.

# ▽ Countdown Calendar flowchart

In this project, the list of important events is created separately from the code as a text file. The program begins by reading in a list of all the events from this file. Once all the days have been calculated and displayed, the program ends.

# ▷ Using Tkinter

The `Tkinter` module is a set of tools that Python programmers use for displaying graphics and getting input from users. Instead of showing output in the shell, `Tkinter` can display results in a separate window that you’re able to design and style yourself.

![](bbox=[0.357, 0.315, 0.535, 0.454])

# Graphical user interface

Tkinter is handy for creating what coders call a GUI (pronounced “gooey”). A GUI (graphical user interface) is the visible part of a program that a person interacts with, such as the system of icons and menus you use on a smartphone. Tkinter creates popup windows that you can add buttons, sliders, and menus to.

![](bbox=[0.032, 0.722, 0.285, 0.957])

A smartphone GUI uses icons to show how strong the WiFi signal is and how much power the battery has.

Start

Get today's date

Get the lists of important events from the text file

Get an event

Calculate the number of days until the event

Display the result

Calculated all events?

N

Y

End