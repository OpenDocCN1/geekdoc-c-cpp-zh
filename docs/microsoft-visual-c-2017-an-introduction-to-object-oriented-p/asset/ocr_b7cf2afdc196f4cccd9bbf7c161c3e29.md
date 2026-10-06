Throughout this book, you have learned how to create interactive GUI programs in which a user can manipulate a variety of Controls. You have worked with several Controls that respond to a user-initiated event, such as a mouse click, and you have provided actions for Control default events. In this chapter, you will expand your understanding of the eventhandling process. You will learn more about the object that triggers an event and the object that captures and responds to that event. You will also learn about delegates—objects that act as intermediaries in transferring messages from senders to receivers. You will create delegates and manage interactive events. You will learn to manage multiple events for a single Control for a project.

# Event Handling

In C#, an event is a reaction to an occurrence in a program; an event transpires when something interesting happens to an object. When you create a class, you decide exactly what is considered "interesting." For example, when you create a Form, you might decide to respond to a user clicking a Button but ignore a user who clicks a Label—clicking the Label is not "interesting" to the Form.

A program uses an event to notify a client when something happens to an object. Events are used frequently in GUI programs—for example, a program is notified when the user clicks a Button or chooses an option from a ListBox. In addition, you can use events with ordinary classes that do not represent GUI controls. When an object’s client might want to know about any changes that occur in the object, events enable the object to signal the client.

> The actions that occur during the execution of the program occur at runtime. The expression at runtime is used to distinguish execution-time activities from those that occur during development time and compile. Events are runtime occurrences.

Because an event is generated when a user interacts with a GUI object, GUI programs are described as event-driven—an event such as a click "drives" the program to perform a task. Programmers say that an action like a button raises an event, fires an event, or triggers an event.

For example, Figure 13-1 shows a Form that contains a Label and a Button. The following changes are the only ones that have been made to the default Form in the IDE:

+   - The Text on the Form has been changed to Event Demo.
- The Size of the Form has been adjusted so the Form will be wide enough for the output it will eventually display.
- A Label has been dragged onto the Form, its Name property has been set to Hello, and its Font has been increased.