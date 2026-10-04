The example displays a small dialog-box-style window with two buttons and a progress bar (refer to Figure 9-1). When you load the solution example into Visual Studio and then build it, run it, and click the upper button, marked Click to Start, the progress bar runs for a few seconds. You see it gradually fill up, one-tenth of its length at a time. When it’s completely full, you can click the Close button to end the program or click Click to Start again.

# Putting the app together

To create the sample app on your own, rather than just load it from the website example — and experience a bit of Windows graphical programming — follow these steps, working first in design mode, where you’re just laying out the appearance of your app.

First create the project and position the necessary controls on your “window”:

+   1. **Choose File→New Project and select Windows on the left, under C#, but this time select Windows Forms Application on the right instead of the usual Console Application; name your project SimpleProgress.**
   The first thing you see is the *form*: a window that you lay out yourself using several *controls*.
2. **Choose View→Toolbox, and from the Toolbox window’s Common Controls group, drag a `ProgressBar` control to the form and drop it; then drag two `Buttons` onto the form.**
3. **Position the buttons and the `ProgressBar` so that they look somewhat like the one shown in Figure 9-1.**
   Note the handy guide lines that help with positioning.

Next, set properties for these controls: Choose View→Properties, select a control on the form, and set the control’s properties:

+   1. **For the progress bar — named `progressBar1` in the code — make sure that the `Minimum` property is 0, the `Maximum` property is 100, the `Step` property is 10, and the `Value` property is 0.**
2. **For the upper button, change the `Text` property to "Click to Start" and drag the sizing handles on the button image until it looks right and shows all its text.**
3. **For the lower button, change the `Text` property to "Close" and adjust the button’s size to your liking.**

In this simple example, you’re putting all code in the *form* class. (The form is your window; its class — here, named `Form1` — is responsible for all things graphical.) Generally, you should put all “business” code — the code that does your calculations, data access, and other important work — in other classes. Reserve the form class for code that’s intimately involved with displaying