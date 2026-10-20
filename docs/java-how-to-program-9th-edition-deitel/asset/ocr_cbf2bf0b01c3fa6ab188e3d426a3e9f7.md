In addition to identifying users, cookies also can indicate users’ shopping preferences. When a Web Form receives a request from a client, the Web Form can examine the cookie(s) it sent to the client during previous communications, identify the user’s preferences and immediately display products of interest to the client.

Every HTTP-based interaction between a client and a server includes a header containing information either about the request (when the communication is from the client to the server) or about the response (when the communication is from the server to the client). When a Web Form receives a request, the header includes information such as the request type and any cookies that have been sent previously from the server to be stored on the client machine. When the server formulates its response, the header information contains any cookies the server wants to store on the client computer and other information, such as the MIME type of the response.

The expiration date of a cookie determines how long the cookie remains on the client’s computer. If you do not set an expiration date for a cookie, the web browser maintains the cookie for the duration of the browsing session. Otherwise, the web browser maintains the cookie until the expiration date occurs. Cookies are deleted by the web browser when they expire.

> **Portability Tip 29.1**
> 
> *Users may disable cookies in their web browsers to help ensure their privacy. Such users will experience difficulty using web applications that depend on cookies to maintain state information.*

# 29.8.2 Session Tracking with @SessionScoped Beans

The previous web applications used @RequestScoped beans by default—the beans existed only for the duration of each request. In the next application, we use a @SessionScoped bean to maintain selections throughout the user’s session. Such a bean is created when a session begins and exists throughout the entire session. A @SessionScoped bean can be accessed by all of the app’s pages during the session, and the app server maintains a separate @SessionScoped bean for each user. By default a session expires after 30 minutes of inactivity or when the user closes the browser that was used to begin the session. When the session expires, the server discards the bean associated with that session.

> **Software Engineering Observation 29.2**
> 
> *@SessionScoped beans should implement the Serializable interface. Websites with heavy traffic often use groups of servers (sometimes hundreds or thousands of them) to respond to requests. Such groups are known as server farms. Server farms often balance the number of requests being handled on each server by moving some sessions to other servers. Making a bean Serializable enables the session to be moved properly among servers.*

# Test-Driving the App

This example consists of a SelectionsBean class that is @SessionScoped and two pages (index.xhtml and recommendations.xhtml) that store data in and retrieve data from a SelectionsBean object. To understand how these pieces fit together, let’s walk through a sample execution of the app. When you first execute the app, the index.xhtml page is displayed. The user selects a topic from a group of radio buttons and submits the form (Fig. 29.17).