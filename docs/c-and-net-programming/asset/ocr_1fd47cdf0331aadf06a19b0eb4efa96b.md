# # HTTP

+   1) Hyper Text Transfer Protocol makes use of the TCP Protocol for communicating with the server. A specific port is being used by this protocol while communicating with the server.
+   2) HTTP provides various methods which represent the actions it will perform while communicating with the server. Some of its methods are "GET", "POST", "DELETE", "HEAD", etc....
+   3) HTTP acts like a bridge between the client and the server as explained below. When user requests a web page, the HTTP Protocol takes the request being sent by the client (using client's browser) and sends it to the server. After receiving the request server locates the requested page and tells the respective website engine to process the request. The website Engine processes the request and sends a response back to the client in an HTML format. Now, HTTP protocol takes the response and sends it to the client which is shown in the client's browser.
+   4) **As HTTP protocol is a stateless protocol**, it is not able to store the state during that session. With each request the objects are created and memory is being allocated and the resources are reclaimed once the server completes its process. Therefore, the cycle of "Create Objects and Utilization of Server Memory" ---- "Process the Request" ---- "Reclaim the Created Resources" continues for each and every user's request. The information given by the user or the State of an Application gets lost during each round trip. In this scenario the State Management is helpful.

# ## 21.15.3 State Management Approaches and Techniques

There are 2 approaches by which ASP.NET manages the state of an application namely,

+   1) Client Side State Management.
+   2) Server Side State Management.

# ### 21.15.3.1 Client Side State Management

+   1) In this method the information added by the user or the information about the user-server interaction is stored on the client's machine or in the page itself. The server resources, like server's memory, are not utilized.
+   2) Bandwidth should be considered while implementing client side state management options because they involve in each roundtrip to server.