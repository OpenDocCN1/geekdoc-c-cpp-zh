properly set:

![](bbox=[0.235, 0.095, 0.765, 0.2])

Now change the URL to localhost:3000/index.js and click Send:

![](bbox=[0.235, 0.248, 0.765, 0.361])

Now change the .js to .pdf in the URL, hit Send and you should get:

![](bbox=[0.235, 0.406, 0.765, 0.511])

Seems as if our Static File Server is working.

Now, go to the Browser and enter in the URL, localhost:3000. This should show the Logon Screen as it used to when we went to port 8000.

Once you have that up, you can try to logon and see what you get.

When I try this, nothing happens. Check the Console to see if there’s any errors besides the fact that we don’t support a favicon.ico.

Here’s what I see:

![](bbox=[0.323, 0.743, 0.677, 0.846])

Click on the index.js:8236 or whatever link is shown at the top of your Stack Trace. That should take you to something like: