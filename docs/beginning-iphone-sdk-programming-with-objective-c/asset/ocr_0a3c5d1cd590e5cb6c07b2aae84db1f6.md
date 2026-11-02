+   7. Save the project and press Command-R to run the application on the iPhone Simulator.
+   8. When the application appears on the iPhone Simulator, click the TextField view. The keyboard should appear. Using the keyboard, type some text into it and press the Return key when you are done. The keyboard now goes away.

# How It Works

What you have just done is connect the Did End on Exit event of the TextField view with the doneEditing: action you have created. When you are editing the content of a TextField view using the keyboard, pressing the Return key on the keyboard fires the Did End On Edit event of the TextField view. In this case, it invokes the doneEditing: action, which contains the following statement:

```
[sender resignFirstResponder];
```

Basically, the sender in this case refers to the TextField view, and resignFirstResponder asks the TextField view to resign its First-Responder status. Essentially, it means that you do not want to interact with the TextField view anymore and that the keyboard is no longer needed. Hence, the keyboard should hide itself.

> NOTE The First Responder in a view always refers to the current view that the user is interacting with. In the example here, when you click the TextField view, it becomes the First Responder and activates the keyboard automatically.

# Set the Keyboard to Number Pad

So far, things have been pretty straightforward. You now know that you can dismiss a keyboard by simply making a TextField resign its First-Responder status. Doing so requires that you handle the Did End On Exit event, which is fired whenever the user clicks the Return key on the keyboard. However, the Return key is shown only when you display it using a non-numeric keyboard type. If you display a numeric keyboard, for example, the Return key is no longer available. In this case, you would have trouble getting the Did End On Exit event to fire.

Therefore, the following Try It Out reaches another technique for dismissing the keyboard, regardless of the type of keyboard displayed.