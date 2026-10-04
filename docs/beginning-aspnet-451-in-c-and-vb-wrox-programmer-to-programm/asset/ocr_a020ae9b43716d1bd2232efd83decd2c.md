# CHAPTER 18 EXCEPTION HANDLING, DEBUGGING, TRACING

Browser Link works best with a multi-monitor setup, or on a large monitor. That enables you to have
multiple browsers open by side. I usually put two or three different browsers on a secondary monitor-
or hit Ctrl+Alt+Enter to come into time while working in Visual Studio to make sure your site still
looks fine in those browsers.

> NOTE The Browser Link implementation in Visual Studio supports communication-
er the server to the browser only. However, the underlying communicationmechanism SignalR supports bidirectional communication. The community
is actively developing plugins to leverage the two-way communication capabilities. One such plugin is the excellent Web Essentials 2013, developed by Mads
Kristensen from the Web Platforms & Tools team at Microsoft. Using that plugin you can make changes to your CSS in the browser, and automatically synchronize those changes back in the source file. You can learn more about Web
Essentials at http://webessentials.com and see a video of Browser Link
CSS editing in action at http://bit.ly/17uo2HI. Note: Visual Studio Express
for Web does not support plugins and you will need a commercial version
of Visual Studio to use this plugin.

Useful as debugging your code web during the development of your site, it lacks the capability
investigate the behavior of your code while it's running in production. Fortunately, ASP.NET has a
solution for that as well: tracing.

# TRACING YOUR ASP.NET WEB PAGES

Without tracing, finding out the values of variables, objects, the execution path that your code follows,
or so on at run is problematic at best. You would probably add a Label control to the page,
and write information to it like this:

**VB.NET**

```
Dim value2 As Double = Convert.ToDouble(ValueBox.Text)
DebugLabel.Text &+= "The value of value2 = &" & value2.ToString() & "<br />"
```

**C#**

```
double value2 = Convert.ToDouble(ValueBox.Text);
DebugLabel.Text += "The value of value2 = " + value2.ToString() + "<br />";
```

Although this certainly works, it's quite cumbersome. You need to write a lot of code to make that
this work. You end up with an ugly Label control in your page that you shouldn't forget
to remove when you're done with your debugging or tracing. And finally, when you're ready,
remove remove all the code that sets the DebugLabel label. You could take the easy way out by
setting the Label control's Visible property to False, but you would still take the performance hit
of assigning the text to the Label control.