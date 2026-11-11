| `javafx.scene.image.ImageView` |
|---|
| • `ImageView(String url)`<br>constructs an image from the given url string. The string should either be a valid construction parameter for the `java.net.URL` class, or a path to a resource. (See Chapter 5 about resources.) |

# ## 13.3 Event Handling

A graphical user interface environment monitors input devices for events such as keystrokes or mouse clicks and directs them to the appropriate program. The program then figures out which user interface control should process the event, translating low-level events to semantic events as appropriate. For example, when a user clicks on a button, JavaFX processes the sequence of events that consists of depressing and releasing the mouse button over the surface of the button control. That event sequence is then interpreted as a “click.”

In order for the program to react to such an event, the programmer needs to register an *event handler* with the user interface control from which the event originates.

# ### 13.3.1 Implementing Event Handlers

In the case of a button click, the event handler must implement the `EventHandler<ActionEvent>` interface. `EventHandler<T>` is a functional interface with a single method

```
void handle(T event)
```

You can simply use a lambda expression to specify the button action:

```
Button button = new Button("Click me!");
button.setOnAction(event -> System.out.println("I was clicked"));
```

In this case, the lambda expression did not make use of the event parameter. An ActionEvent doesn’t have many interesting properties. The most useful one is probably the event source—the control from which the action originated. In this case, we know which button is the source. However, if you share one handler among multiple controls, you can call event.getSource() to find out which one triggered it.

Here is another application of event handling where you are interested in the event object. When the user closes a window, the window gets a “close