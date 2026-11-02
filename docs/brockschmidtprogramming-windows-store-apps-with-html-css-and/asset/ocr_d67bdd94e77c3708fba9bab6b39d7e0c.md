like controls and other UI elements!

Of course, the real creative effort to find new ways to use online content is both your challenge and your opportunity. What we can cover in this chapter are simply the tools that you have at your disposal for that creativity.

We'll begin with the essential topic of network connectivity, because there's not much that can be done without it! Then we'll explore the options for directly hosting dynamic web content within an app's own UI, as is suitable for many scenarios. Then we'll look at the APIs for HTTP requests, followed by those for background transfers that can continue when an app is suspended or not running at all. We'll then wrap up with the very important subject of authentication, which includes working with the user's Microsoft account, user profile, and Live Connect services.

One part of networking that we won't cover here is sockets, because that's a lower-level mechanism that has more context in device-to-device communication. We'll come back to that in Chapter 17, "Devices and Printing." Similarly, setting up service connections for live tiles and push notifications are covered in Chapter 16, "Alive with Activity." The subject of roaming app state is something we'll pick up in Chapter 10, "The Story of State, Part 1," and navigating to and choosing files from network shares has context with the file pickers that we'll see in Chapter 11, "The Story of State, Part 2."

And there is yet more to say on some web-related and networking-related subjects, but I didn't want those details to intrude on the flow of this chapter. You can find those matters in Appendix C, "Additional Networking Topics."

# Sidebar: Debugging Network Traffic with Fiddler

Watching the traffic between your machine and the Internet can be invaluable when trying to debug networking operations. For this, check out the freeware tool from Telerik called Fiddler (http://fiddler2.com/get-fiddler). In addition to inspecting traffic, you can also set breakpoints on various events and fiddle with (that is, modify) incoming and outgoing data.

# Sidebar: Windows Azure Mobile Services

No discussion of apps and services is complete without giving mention to the highly useful features of Windows Azure Mobile Services, especially as you can start using them for free and start paying only once your apps become successful and demand more bandwidth.

+   - **Data:** easy access to cloud-based table storage (SQL Server) without the need to use HTTP requests or other low-level mechanisms. The client-side libraries provide very straightforward APIs for create, insert, update, and delete operations, along with queries. On the server side, you can attach node.js scripts to these operations, allowing you to validate and adjust the data as well as trigger other processes if desired.