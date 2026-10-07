# The handler 4

The handler at its core, is what handles the incoming request for a specific route. It determines how the request will be “handled.” The configuration for the route plays a critical part in how the handler needs to behave, and since it's tightly coupled, some configuration for the route needs to be taken into consideration.

When we specify a route for a request, for example, if you're going to download a file from /downloads/<filename> then it is the handler that has all of the logic in it for finding the file in question in order to send it to the connecting client. The handler may also do other things, like counting how many times the file has been downloaded, access control making sure not just anyone has access to download the file, and so on.

The handler function “handles” all of the decisions and logic between accepting a request from the client and returning a response to the user. haki has some nice features to offload some work automatically, such as validation. We will look at this in more detail in Chapter 5 (why would we dream of doing that though?)

The handler is generally a callback function that is comprised of two arguments: the request and the reply. There are multiple other-built-in handlers that we will also go over and discover.

This chapter will cover the various use-cases for the handler. We're going to delve into the arguments of the handlers and various methods for making life in the handler easier for ourselves.

# The request

The request object contains all of the information pertaining to the incoming request to the server whether it be from a browser, or some other tool using the API. Since the routing already determines which request will be handled depending on the method, the request received will be limited to whatever is specified. At the end of the day, the full request is available here, which contains the headers and all of the data content sent.

Refer back to the request object to find out how the request travels through the framework.