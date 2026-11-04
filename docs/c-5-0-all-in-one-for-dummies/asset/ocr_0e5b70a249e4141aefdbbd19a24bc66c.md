# Chapter 4: Practical WPF

# In This Chapter

+   - Using built-in and customized commands
+   - Writing adequate unit tests
+   - Working with the ViewModel

Even though WPF still supports the direct event handler wire up (for example, through the OnClick event), WPF introduces a much better mechanism for responding to user events. It significantly reduces the amount of code you have to write and adds testability to your application. Traditional event handling is all contained in the code-behind for your form, which is extremely difficult to test in an automated fashion.

Software patterns have been around for a long time, first brought to the forefront by the classic tome Design Patterns: Elements of Reusable Object-Oriented Software (Addison-Wesley) by Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides — commonly referred to as the “Gang of Four.” Software has evolved, and many new patterns have been developed over the years. One of the most effective user interface patterns developed for WPF is the Model-View-View Model pattern (commonly referred to as ViewModel). Using the ViewModel pattern in your WPF applications will improve software reuse, testability, readability, maintainability, and most of the other “-ilities” as well. (You run across other design patterns throughout this whole book.)

# Commanding Attention

The Command Pattern has been around since, well, forever, and you most likely use it every day. Copy and Paste commands are example implementations of the pattern built into Windows and most Windows applications. WPF provides a significant number of built-in commands and also allows for completely customized commands!

Traditional handling of user events (and still supported in WPF) is through an event handler. When the button on the Window is clicked, the code in the event handler (which has to be in the code-behind file) will execute. By placing this code in the code-behind event handler, the business logic is now mixed with the user interface code, mixing concerns. To be fair, nothing in