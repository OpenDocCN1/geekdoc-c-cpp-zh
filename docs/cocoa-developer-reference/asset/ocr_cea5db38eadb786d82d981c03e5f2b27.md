![](bbox=[0.089, 0.031, 0.202, 0.123])

# # Building Dashboard Widgets

![](bbox=[0.092, 0.154, 0.928, 0.191])

Widgets were introduced in 2005 in OS X 10.4 Tiger. Like iPhone apps, widgets offer users a simple, accessible benefit in a stylish wrapper. Some widgets provide unit or currency conversions or utilities such as clocks, calculators, and countdown timers. Others package entertainment — cartoons are a popular choice — or Web information, such as traffic reports or weather. And widget games are always popular.

Users continue to find widgets fascinating because they make it easy to customize a Mac with a unique collection of attractively packaged micro-applications.

The look and feel of widgets is based very loosely on Yahoo!'s Konfabulator project, which was formerly sold as a separate OS X application. Internally, widgets use JavaScript, HTML, and CSS, but include links to elements of Cocoa, and can be extended with plug-ins written in Objective-C.

# ## Introducing Dashboard

Widgets load and run automatically within Dashboard — the widget manager application. Dashboard, shown in Figure A.1, runs permanently as an OS X background task. It remains hidden until the user activates it by typing a function key or moving the mouse cursor to one of Exposé’s hot corners.

To the user, Dashboard is somewhat like an alternative desktop. A selection of widgets appears in the Dashboard area, where they can be repositioned by clicking and dragging.

Clicking the Open (+) button at the bottom left of the Dashboard area displays a dock-like menu that lists all installed widgets. Choosing a widget in the dock copies it to the Dashboard “desktop” and installs it with an attractive ripple-like animation, illustrated in Figure A.2.

+   **In This Appendix**
+   
+   - Introducing Dashboard
+   - Profiting from widgets
+   - Understanding widget technology
+   - Introducing Dashcode
+   - Building a widget in Dashcode