# PUT ON YOUR THINKING HAT...

Try out triggers by adding some to the FluentDictionary we've been working with.

+   1. Add a trigger to the TextBox that sets the FontStyle to Italic when it has focus. The trigger property isn't IsSelected. What is it? (You can check MSDN or the object browser for the list of properties exposed by the TextBox class.)

+   2. Add a trigger to the Button style that changes the FontWeight to Bold and the FontStyle to Italic when the button is pressed.

+   3. Write a trigger for the button that reverses the gradient when IsMouseOver is true. Hint: You need to change the starting and ending points, but you can use the same collection of steps.
+   
+   The trigger won't quite work. We won't be able to fix it until we look at control templates in the next chapter, but can you identify the problem? (You might not be able to if you have a really, really fast machine.)

+   4. Triggers are applied when the specified property has the specified value. What happens when the value is no longer true? (To test this, try tabbing in and out of one of the TextBox elements on our sample window.