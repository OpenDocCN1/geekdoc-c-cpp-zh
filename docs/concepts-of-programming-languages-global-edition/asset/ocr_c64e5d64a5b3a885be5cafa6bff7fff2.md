An exception handler is specified with a rescue clause, which is attached to a statement. To attach an exception handler to a segment of code, the code is placed in a begin-end block. The rescue clause is placed in the block after the code of the block. In general, this appears as in the following:

```
begin
    The sequence of statements in the block
rescue
    The handler
end
```

A begin-end block can include an else clause and/or an ensure clause. The else clause is exactly like that of Python. The ensure clause is exactly like a finally clause. A method can act as a container for exception handling in place of a begin-end block.

In a clear departure from most other languages, Ruby allows a segment of code that raised an exception to be rerun after the exception is handled. This is specified with a retry statement at the end of the handler.

# 14.5 Introduction to Event Handling

Event handling is similar to exception handling. In both cases, the handlers are implicitly called by the occurrence of something, either an exception or an event. While exceptions can be raised either explicitly by user code or implicitly by hardware or a software interpreter, events are created by external actions, such as user interactions through a graphical user interface (GUI). In this section, the fundamentals of event handling, which are less complex than those of exception handling, are introduced.

In conventional (non-event-driven) programming, the program code itself specifies the order in which that code is executed, although the order is usually affected by the program's input data. In event-driven programming, parts of the program are executed at completely unpredictable times, often triggered by user interactions with the executing program.

The particular kind of event handling discussed in this chapter is related to GUIs. Therefore, most of the events are caused by user interactions through graphical objects or components, often called widgets. The most common widgets are buttons. Implementing reactions to user interactions with GUI components is the most common form of event handling.

An event is a notification that something specific has occurred, such as a mouse click on a graphical button. Strictly speaking, an event is an object that is implicitly created by the run-time system in response to a user action, at least in the context in which event handling is being discussed here.

An event handler is a segment of code that is executed in response to the appearance of an event. Event handlers enable a program to be responsive to user actions.