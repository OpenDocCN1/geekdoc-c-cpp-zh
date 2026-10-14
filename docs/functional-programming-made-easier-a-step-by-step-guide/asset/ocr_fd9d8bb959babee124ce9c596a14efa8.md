Now, we just need a way to test an HTTP POST request.

There’s a very good tool called Postman that let’s you send requests to servers. It’s great for testing APIs.

Go to the Postman Download Page and download and install Postman.

Then run it. If it asks you to sign in, simply select the grey text to Skip. Now, click on the Plus Icon near the top of the window:

![](bbox=[0.433, 0.218, 0.567, 0.293])

Then you’ll get a new tabbed pane:

![](bbox=[0.146, 0.342, 0.853, 0.497])

Pulldown the menu next to GET and choose POST and then enter localhost:3000/hello into the Request URL Field.

Then click Send and if your server is still running, you should see:

![](bbox=[0.146, 0.599, 0.853, 0.883])

Down at the bottom is our response, hello.

Let’s make a slight change to our router Function to parse path segments: