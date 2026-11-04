Data binding tells a control what member of the underlying class to get its data from. For instance, if you have a collection of Apple objects with a property of Color that you want to show in a text box, you can bind the value Apple.Color to the Text property.

But things get more interesting than that. Let's say that you want to provide a list of colors and allow the user to select the color of the object in question. You can do that by binding the list of a collection and the selected value to the SelectedItem property of the list control. If you want to show the color itself, you can bind to the FontColor property of a text control.

# Setting up your markup for binding

Back in the Active Server Page days, you put all your data on the page by simply printing it there. Sounds simple but it had a lot of problems. Foremost, your form had to have a lot of knowledge about the data it was showing. This is a bad thing. Anyway, the format for doing it was

```
<%= ThisIsWhatIWantToPrint %>
```

If you needed a list, you looped in the surrounding code. If you needed a method result, you just put the method right in there. What you saw was what you got.

Data binding is the more enlightened form of getting data on the screen. The controls that are built into ASP.NET know how to handle data on their own, so long as that data meets some basic specifics.

Data binding is accomplished by setting a property of a control to a member of the underlying class. For a single control, like a text box, you just set the property in question, like this:

```
<asp:Label ID="Label1" runat="server" Text='<%# IAmBindingToThisVariable %>' />
```

If you are binding to a repeating control, like a Grid or a ListBox, then you set the DataSource property. I show you how to do that in the next section, "Bindings in code."

The variables you are binding to need to be in the code-behind, and be public. If they aren't, you will get runtime errors. That's also why binding in the code is a good idea, which we do in the next section.

Right now, let's talk binding in the markup. Here's all you need to do to set up your markup for binding:

![](bbox=[0.05, 0.78, 0.18, 0.9])