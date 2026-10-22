```
irb(main):004:0> pr.save
=> true
```

Logging and tracing are a great way of understanding the dynamics of complex applications. You'll find a wealth of information in the development log file. When something unexpected happens, this should probably be the first place you look. It's also worth inspecting the web server log for anomalies. If you use WEBrick in development, this will be scrolling by on the console you use to issue the script/server command.

You can add your own messages to the log with the Logger object described in the previous section. Sometimes the log files are so busy that it's hard to find the message you added. In those cases, if you're using WEBrick, writing to STDERR will cause your message to appear on the WEBrick console, intermixed with the normal WEBrick tracing.

If a page comes up displaying the wrong information, you might want to dump out the objects being passed in from the controller. The debug helper method is good for this. It formats objects nicely and makes sure that their contents are valid HTML.

```
<h3>Your Order</h3>

<%= debug(@order) %>

<div id="ordersummary">
  ...
</div>
```

Finally, for those problems that just don't seem to want to get fixed, you can roll out the big guns and point irb at your running application. This is normally available only for applications in the development environment.

To use breakpoints, follow these steps:

+   1. Insert a call to the method debugger at the point in your code where you want your application to first stop.

+   2. On a convenient console, start the server with the -u or --debugger argument, like this.³

```
depot> ruby script/server -u
=> Booting WEBrick...
=> Debugger enabled
=> Rails application started on http://0.0.0.0:3000
```

+   3. Using a browser, prod your application in order to make it hit the debugger method. When it does, the console where the script/server is running

3. You need to install ruby-debug to run the server in debugging mode. With gems, use gem install ruby-debug.