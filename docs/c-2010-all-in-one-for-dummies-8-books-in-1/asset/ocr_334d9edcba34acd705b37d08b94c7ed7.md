# Working in Visual Studio

in Chapter 1, there is no real state management on these controls — it is all faked by the ViewState variable in the HTML, and if you overuse the ViewState, you will have a slow application.

# Adding some [functionality] using C#

Let's start by making the form to do something. Code View basically allows the developer to write code that does something useful with the Web form. Here I keep it, but it can get much more complex.

There is already an event handler for the Button.Click event so I suggest you use that method to change the text of the Label. This is a common operation in Web applications. The label ID was TextToChange, so you need to add this code:

```
ToChange.Text = "It has changed";
```

That was simple. You need to know that this will be the simplest event handler that you will ever write, however. They get harder.

Run the application by pressing <F5>. (If neither of us made a mistake, it should build.) Then launch the Cassini server, and then your browser will launch. Click the Click Me button, and your screen should look like the one in Figure 2-4.

![](bbox=[0.235, 0.558, 0.825, 0.915])

Figure 2-4:
Hey, it worked!