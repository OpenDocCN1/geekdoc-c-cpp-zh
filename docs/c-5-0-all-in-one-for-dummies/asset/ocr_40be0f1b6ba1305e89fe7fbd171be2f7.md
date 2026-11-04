But things get more interesting than that. Say that you want to provide a list of colors and allow the user to select the color of the object in question. You can do that by binding the list of a collection and the selected value to the SelectedItem property of the list control. If you want to show the color itself, you can bind to the FontColor property of a text control.

# Setting up your markup for binding

Back in the Active Server Page days, you put all your data on the page by simply printing it there. Sounds simple, but it had a lot of problems. Foremost, your form had to have a lot of knowledge about the data it was showing. This is a bad thing. Anyway, the format for doing it was

```
<%= ThisIsWhatIWantToPrint %>
```

If you needed a list, you looped in the surrounding code. If you needed a method result, you just put the method right in there. What you saw was what you got.

Data binding is the more enlightened form of getting data on the screen. The controls that are built into ASP.NET know how to handle data on their own, so long as that data meets some basic specifics.

Data binding is accomplished by setting a property of a control to a member of the underlying class. For a single control, like a text box, you just set the property in question, like this:

```
<asp:Label ID="Label1" runat="server" Text="<%# IAmBindingToThisVariable %>" />
```

If you're binding to a repeating control, like a Grid or a ListBox, then you set the DataSource property. I show you how to do that in the next section.

![](bbox=[0.15, 0.68, 0.25, 0.82])

The variables you are binding to need to be in the code-behind and be public. If they aren't, you will get runtime errors. That's also why binding in the code is a good idea, which I do in the next section.

Right now, I'll talk binding in the markup. Here's all you need to do to set up your markup for binding:

+   1. **In the Chapter 3 web project that you've been adding pages with controls to, right-click and choose Add, New Item, and then Class.**
+      I named my class Show.
+   2. **Click OK and then put this simple data class in there.**
+      This class is just for example — it could be a database or a data class or an Entity Framework model.