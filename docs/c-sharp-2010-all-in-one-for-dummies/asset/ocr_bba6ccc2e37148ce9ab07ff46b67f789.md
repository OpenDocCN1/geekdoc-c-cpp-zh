+   2. For the upper button, change the Text property to "Click to Start" and drag the sizing handles on the button image until it looks right and shows all its text.
+   
+   3. For the lower button, change the Text property to "Close" and adjust the button's size to your liking.

![](bbox=[0.14, 0.26, 0.24, 0.4])

In this simple example, you're putting all code in the form class. (The form is your window; its class — here, named Form1 — is responsible for all things graphical.) Generally, you should put all "business" code — the code that does your calculations, data access, and other important work — in other classes. Reserve the form class for code that's intimately involved with displaying elements on the form and responding to its controls. I break that rule here — but the delegate works no matter where its callback method is.

Now, still in design mode, add a handler method for each button:

+   1. On the form, double-click the new Close button.

This action generates a method in the "code behind the form" (or, simply, "the code-behind") — the code that makes the form work. It looks like this — you add the boldfaced code:

```
private void button2_Click(object sender, EventArgs e)
{
    this.Close(); // 'this' refers to the Form1 class.
}
```

![](bbox=[0.14, 0.7, 0.24, 0.84])

To toggle between the form's code and its image, choose View→Code or View→Designer.

+   2. Double-click the new Click to Start button to generate its handler method, which looks like the following in the code-behind:

```
private void button1_Click(object sender, EventArgs e)
{
    UpdateProgressCallback callback = UpdateProgressCallback(this.DoUpdate);
    // Do something that needs periodic progress reports.
    // This passes a delegate instance that knows how to update the bar.
    DoSomethingLengthy(callback);
    // Clear the bar so that it can be used again.
    progressBar1.Value = 0;
}
```

+   3. Add the following callback method to the form class:

```
private void DoUpdate()
{
    progressBar1.PerformStep(); // Tells progress bar to update itself
}
```

I walk you through the remaining code, all of it on the form class, in the next section. Later in the chapter, I show you other variations on the delegate that's passed.