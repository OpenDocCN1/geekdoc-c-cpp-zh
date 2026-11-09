
You can then access the front object’s properties using standard dot syntax. To set a custom ID for a part, type the ID name into the ID field in the Attributes pane in the Inspector. Each part includes a fixed list of accessible properties via DOM. Some, but unfortunately not quite all, properties are listed and described in the Dashcode User Guide. To view the User Guide, choose Help ➜ Dashcode User Guide.

DOM is an essential part of widget management. Use it to change basic properties, such as text strings, or to swap objects in and out of visibility. Some parts, such as the Canvas, have more sophisticated interfaces; for example, you can draw into a Canvas using JavaScript versions of standard canvas functions.

## Working with Events and Handlers

As in an Objective-C application, visible parts in a widget can be connected to handler functions that are triggered when the user clicks with a mouse, drags an object, and so on. For example, a part’s onclick event is triggered when the user clicks the object. The list of events for each object or part is visible in the Behaviors pane in the Inspector.

To assign a Handler, select an event and double-click in the area under the Handler header to its right. An empty box appears. To finish the assignment, type the name of the handler routine into the box, as shown in Figure A.11. There is no hinting, and no menu or list of possible handlers — you must type the name in manually. You can check that your assignment is correct by clicking the arrow to the right of the handler name; the corresponding code routine is highlighted in light blue.

Figure A.11

Because the Handler field is dumb, you must type in the function name manually. If you get it wrong, the Event won’t trigger correctly.

![](img/2b293e29fc15b0797f113b85dd429b6e_581_0.png)

### Working with widget events

Widget templates typically include code to create a spin effect triggered by clicking the Info part, typically in the showFront(event) and showRear(event) routines. You won't usually need to change this code, but you can add parts to the reverse of the widget with custom handlers of your own design — for example, to ask for a donation with a link to your Web site.

At the bottom of every template is a boilerplate conditional:

```javascript
if (window.widget) {
    widget.onremove = remove;
    widget.onhide = hide;
    widget.onshow = show;
    widget.onsync = sync;
}
```

This assigns custom handler functions — hide, remove, show, sync — to standard widget events that are triggered when Dashcode changes state. Stubs for each custom handler are included at the top of the template scripts. You can add extra code to these stubs to enable or disable widget features as needed for each state.

### Working with time

Many widgets use timers, but JavaScript lacks a simple drop-in equivalent for NSTimer. To create a timer, use:

```javascript
aTimer = setInterval(aFunctionCalledWhenTheTimerExpires,
                     aTimeInMilliseconds);
```

This calls aFunctionCalledWhenTheTimerExpires after aTimeInMilliseconds. Timer functions can call themselves for repeated timing events. To stop a timer and delete it, use

```javascript
clearInterval(aTimer);
aTimer = null;
```

To get the current time, use the Date() function:

```javascript
var currentTime = new Date();
var currentHours = currentTime.getHours();
var currentSeconds = currentTime.getSeconds();
```

### Loading images

Images can be preloaded for speed with

```javascript
(new Image()).src = "/Images/anImage.png";
var anImage = new Image(width, height);
anImage.src = "/Images/anImage.png";
```

You can then write or link an image into any part in the widget or draw it to a canvas.

![](img/2b293e29fc15b0797f113b85dd429b6e_586_0.png)

## Maximizing Productivity and Avoiding Errors

![](img/2b293e29fc15b0797f113b85dd429b6e_586_1.png)

Software development can be rewarding, but it can also be frustrating. Most developers have the experience of code that refuses to work for days or weeks as various possible solutions are tried and discarded.

Many solo projects are improved rather than developed in a structured way. The reliability of formal project management in commercial software engineering is inconsistent, and no technique or process can guarantee that a project will be completed on time or on budget. But as a solo developer, you can use simple check-lists and hold discussions with other developers to make your projects less stressful, more productive, and less time consuming.

### Managing Projects Successfully

Three simple project management techniques can dramatically improve your productivity:

- **Use source code management and version control.** Even the simplest projects can benefit from the version control features built into Xcode and introduced in Chapter 3 of this book. You can use them to roll back major coding or design mistakes, without losing other work.

- **Produce reference documentation as you go.** Reference documentation, includes notes and object diagrams, takes almost no time to produce but is a tested and proven way to clarify design. If your ideas are clear, your code is more likely to be correct, and the application is more likely to work as you want it to. With a free tool such as doxygen — from www.doxygen.org and illustrated in Figure B.1 — you can build reference documentation as you code by writing it directly into comment fields.

- **Eliminate compiler errors with a checklist of standard solutions.** Many errors are caused by a small number of simple mistakes. You can eliminate them by working through a formal error checklist.

| In This Appendix |
|---|
| Managing projects successfully |
| Getting help |
| Solving impossible problems |

Figure B.1

Doxygen was developed to simplify documentation, and it can translate comments and notes into a variety of document formats.

![](img/2b293e29fc15b0797f113b85dd429b6e_587_0.png)

### Solving common problems

Tables B.1 and B.2 list some of the more common syntax and build errors. If you find yourself making other repetitive errors, add them to a list. Many developers repeat the same mistakes; if you list yours, it can help condition you to avoid them.

**Table B.1 Common Syntax Errors**

| Error type | Description |
|---|---|
| Missing semicolon | This is common, but it’s easy to spot. Xcode flags it on the next line with an `Expected ';' ...` error. |
| Missing or extra curly bracket | Xcode’s bracket balancing doesn’t always catch this error, which typically causes multiple error messages in a single file. Look for `Expected declaration or statement at end of input` at the end of a file and work back to find the first unbalanced method. The missing bracket is usually in the method above it. |
| Missing or extra square bracket | This is another simple mistake that can cause multiple error messages. Look for `Expected ']' ...` on the line with the missing bracket. |
| Missing or extra capitalization | This is one of the most common errors in Objective-C, and it can be very easy to miss. Look for properties, variables, and methods that appear correct but aren’t recognized by the compiler. Triple-check capitalization around the error. Check again wherever the word `view`, or one of its compounds, such as `Superview`, appears; they’re often wrongly capitalized in method names. |
| Missing or extra colon in a method name | Remember that `aMethod:` and `sameMethod` are unrelated and distinct. Avoid declaring methods with easily confused names. Look for crashes and console messages warning that a selector wasn’t found. |
| Missing or extra parameters in method calls | A popular mistake is to create a custom method based on a system method with added extra parameters in a class prototype, and then call the original unaltered method in the class implementation. Avoid this by creating a formal category. |
| `[anObject = aMethod[etc];` | Assignments within square brackets are usually syntax errors. Avoid them even where they’re nominally correct by breaking out the assignment onto a separate line. |
| `if (a==b)...` | Everyone does this—usually more than once. |
| `if (aString == bString) ...` | Use `isEqual:`, or one of its typed equivalents, when comparing objects. The standard comparison compiles and runs without error, but compares pointer addresses instead of object content. |
| Incomplete subproperty lists | Common for complex object with many subproperties—for example, `window.width` instead of `window.frame.size.width`. Look for the famous `Request for member 'property' in something not a structure or union` message. |

![](img/2b293e29fc15b0797f113b85dd429b6e_588_0.png)

**TIP**

You can avoid subproperty errors by creating a reference list of common objects and their subproperties. It can be difficult to remember complete subproperty lists — a reference can save you hours of time.
