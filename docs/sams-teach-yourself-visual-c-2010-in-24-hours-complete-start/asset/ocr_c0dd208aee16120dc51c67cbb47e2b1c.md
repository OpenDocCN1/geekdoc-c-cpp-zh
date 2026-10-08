+   3.  Add a class named Contact that looks like the one shown in Listing 6.5.

+   4.  Run the application by pressing Ctrl+F5. The output should look like Figure 6.8. Make sure to set the PublishAndRaise project as the startup project.

![](bbox=[0.23, 0.21, 0.64, 0.31])

![](bbox=[0.78, 0.19, 0.94, 0.33])

# # Summary

In this hour, you learned how C# enables you to create highly interactive applications by raising and responding to events. You also learned that events are not just about user interaction through a graphical user interface but that events also provide a rich and sophisticated notification system that your classes can use.

Through the Visual Studio 2010 editor, you have seen how easy it is to create your own event handlers for responding to events initiated through the user interface.

# # Q&A

**Q. What is a delegate?**

**A.** A delegate is a type-safe and secure way of writing a callback, similar to a C++ function pointer or Delphi closure. Using a delegate allows you to encapsulate a reference to a method. The code that calls the referenced method does not need to know at compile time which method will be invoked. Delegates run under the caller's security permissions, not the declarer's permissions.

**Q. What is an event?**

**A.** An event is any external stimulus to a program, such as user actions (mouse clicks or key presses), messages from other programs, or parts of the same programs.

**Q. What is the EventArgs class?**

**A.** The EventArgs class stores data for an event. Although it can be used directly, it is best to derive a new class for your event, even if it is initially empty.