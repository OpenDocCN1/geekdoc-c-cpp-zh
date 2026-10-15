This isn’t the end of it. As you’ll note in Figure 1-29, by clicking on the down arrows you see on the right hand side of your new custom watch window, just below the pin, you can add one or more comments to your custom watch window for this value. You also have the option to unpin the initial placement of this window and move it off of your Code view display. Not only that but, the custom watch window is persistent in Debug mode. If you stop debugging and restart, the window is automatically restored and remains available until you choose to close it using the close button.

Next, move your mouse and hover over the parameter sender. This will open a window similar to the one for Count as you review the reference to this object. More important, note the small plus sign on the right-hand side, which if clicked expands the pop-up to show details about the properties of this object. As shown in Figure 1-30, this capability is available even for parameters like sender, which you didn’t define. Figure 1-30 also illustrates a key point about looking at variable data. Notice that by expanding the top-level objects you can eventually get to the properties inside those objects. Next to some of those properties, on the right-hand side, is a little magnifying glass icon. That icon tells you that Visual Studio will open the potentially lengthy string value in any one of three visualization windows. When working with complex XML or other complex data, these visualizers offer significant productivity benefits by enabling you to review data.

![](bbox=[0.14, 0.32, 0.8, 0.68])

FIGURE 1-30

Once you are at a breakpoint, you can control your application by leveraging the Debug buttons on the Standard toolbar. These buttons, shown in Figure 1-31, provide several options for managing the flow of your application. From the left are the following buttons: Start Debugging, Break All, Stop Debugging, and three buttons that look like a carriage return next to a set of lines. The first of these, which is the fourth button overall represents stepping into code. The last two buttons represent stepping over and stepping out, respectively. In this case you should use the Step Into or Step Over buttons to move to the next line of code as shown in Figure 1-29.

![](bbox=[0.79, 0.7, 0.93, 0.73])

FIGURE 1-31

Step-In tells the debugger to jump to whatever line of code is first within the next method or property you call. Keep in mind that if you pass a property value as a parameter to a method, then the first such line