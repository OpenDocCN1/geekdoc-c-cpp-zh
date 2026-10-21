![](bbox=[0.25, 0.09, 0.69, 0.34])

Figure 11-4

Note that the window has a number of properties provided by the operating system that require no programming effort on your part to manage. The boundaries of the window can be dragged to resize it, and the whole window can be moved about onscreen. The maximize and minimize buttons also work. Of course, all of these actions do affect the program. Every time you modify the position or size of the window, a WM_PAINT message is queued and your program has to redraw the client area, but all the work of drawing and modifying the window itself is done by Windows.

The system menu and Close button are also standard features of your window because of the options that you specified in the WindowClass structure. Again, Windows takes care of the management. The only additional effect on your program arising from this is the passing of a WM_DESTROY message if you close the window, as previously discussed.

# Windows Program Organization

In the previous example you saw an elementary Windows program that used the Windows API and displayed a short quote from the Bard. It’s unlikely to win any awards, being completely free of any useful functionality, but it does serve to illustrate the two essential components of a Windows program: the WinMain() function that provides initialization and setup, and the WindowProc() function that services Windows messages. The relationship between these is illustrated in Figure 11-5.

It may not always be obvious in the code that you will see, but this structure is at the heart of all Windows programs. Understanding how Windows applications are organized can often be helpful when you are trying to determine why things are not working as they should be in an application. The WinMain() function is called by Windows at the start of execution of the program and the WindowProc() function, which you’ll sometimes see with the name WndProc(), is called by the operating system whenever a message is to be passed to your application’s window. In general there typically is a separate WindowProc() function in an application for each window in an application.