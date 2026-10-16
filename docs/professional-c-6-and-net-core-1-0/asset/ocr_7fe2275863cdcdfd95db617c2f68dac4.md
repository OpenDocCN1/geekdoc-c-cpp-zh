![](bbox=[0.105, 0.062, 0.894, 0.255])

# Figure 19.12

Now you can run the UI test in the same way you run the unit tests, as shown earlier in this chapter.

# Web Testing

To test web applications, you can create unit tests that invoke methods of the controllers, repository, and utility classes. Tag helpers are simple methods in which the test can be covered by unit tests. Unit tests are used to test the functionality of the algorithms of the methods—in other words, the logic inside the methods. With web applications, it is also a good practice to create performance and load tests. Does the application scale? How many users can the application support with one server? How many servers are needed to support a specific number of users? Which bottleneck is not that easy to scale? To answer these questions, Web tests can help.

With Web tests, HTTP requests are sent from the client to the server. Visual Studio also offers a recorder that needs an add-in within Internet Explorer. At the time of this writing, Microsoft Edge cannot be used as a recorder because this browser currently doesn’t support add-ins.

# Creating the Web Test

For creating a Web test, you can create a new ASP.NET Web Application with ASP.NET Core 1.0 named WebApplicationSample. This template has enough functionality built in that allows for creating tests. To create Web tests, you add a Web Performance and Load Test Project named WebAndLoadTestProject to the solution. Click on the WebTest1.webtest file to open the Web Test Editor. Then start a Web recording by clicking the Add Recording button. For this recording, you must have the Web Test Recorder add-in with Internet Explorer that’s installed with the installation of Visual Studio. The recorder records all HTTP requests sent to the server. Click some links on the WebApplicationSample web application such as About and Context, and register a new user. Then click the Stop button to stop the recording.

After the recording is finished, you can edit the recording with the Web