
![](img/009e962758dcc71dbc43a493362e6dc0_1276_0.png)

Fig. 29.2 | Client interacting with the web server. Step 2: The HTTP response.

informs the client that the web server could not locate the requested resource. On a successful request, the server appends the requested resource to the HTTP response. A complete list of numeric codes indicating the status of an HTTP transaction can be found at www.w3.org/Protocols/rfc2616/rfc2616-sec10.html.

### HTTP Headers

The server then sends one or more HTTP headers, which provide additional information about the data that will be sent. If the server is sending an HTML text document, one HTTP header would read:

```
Content-type: text/html
```

The information provided in this header specifies the Multipurpose Internet Mail Extensions (MIME) type of the content that the server is transmitting to the browser. MIME is an Internet standard that specifies data formats so that programs can interpret data correctly. For example, the MIME type text/plain indicates that the sent information is text that can be displayed directly, without any interpretation of the content as HTML markup. Similarly, the MIME type image/jpeg indicates that the content is a JPEG image. When the browser receives this MIME type, it attempts to display the image. For a list of available MIME types, visit www.w3schools.com/media/media_mimeref.asp.

The header or set of headers is followed by a blank line, which indicates to the client browser that the server is finished sending HTTP headers. The server then sends the contents of the requested resource (such as, downloads.html). In the case of an HTML document, the web browser parses the HTML markup it receives and renders (or displays) the results.

### HTTP GET and POST Requests

The two most common HTTP request types (also known as request methods) are GET and POST. A GET request typically asks for a resource on a server. Common uses of GET requests are to retrieve an HTML document or an image or to fetch search results from a search engine based on a user-submitted search term. A POST request typically sends data to a server. Common uses of POST requests are to send form data or documents to a server.

When a web page contains an HTML form in which the user can enter data, an HTTP request typically posts that data to a server-side form handler for processing. For example, when a user performs a search or participates in a web-based survey, the web server receives the information specified in the form as part of the request.

GET requests and POST requests can both send form data to a web server, yet each request type sends the information differently. A GET request sends information to the server in the URL, as in www.google.com/search?q=deitel. Here, search is the name of Google’s server-side form handler, q is the name of a variable in Google’s search form and deitel is the search term. A ? separates the query string from the rest of the URL in a request. A name/value pair is passed to the server with the name and the value separated by an equals sign (=). If more than one name/value pair is submitted, each is separated from the next by an ampersand (&). The server uses data passed in a query string to retrieve an appropriate resource. The server then sends a response to the client. A GET request may be initiated by submitting an HTML form whose method attribute is set to "get", by typing the URL (possibly containing a query string) directly into the browser’s address bar or through a hyperlink when the user clicks the link.

A POST request sends form data as part of the HTTP message, not as part of the URL. The specification for GET requests does not limit the query string’s number of characters, but some web browsers do (for example, Internet Explorer restricts the length to 2083 characters), so it’s often necessary to send large pieces of information using POST. Sometimes POST is preferred because it hides the submitted data from the user by embedding it in an HTTP message.

### Software Engineering Observation 29.1

> The data sent in a POST request is not part of the URL, and the user can’t see the data by default. However, tools are available that expose this data, so you should not assume that the data is secure just because a POST request is used.

### Client-Side Caching

Browsers often cache (save on disk) web pages for quick reloading. If there are no changes between the version stored in the cache and the current version on the web, the browser uses the cached copy to speed up your browsing experience. An HTTP response can indicate the length of time for which the content remains “fresh.” If this amount of time has not been reached, the browser can avoid another request to the server. Otherwise, the browser requests the document from the server. Thus, the browser minimizes the amount of data that must be downloaded for you to view a web page. Browsers typically do not cache the server’s response to a POST request, because the next POST might not return the same result. For example, in a survey, many users could visit the same web page and answer a question. The survey results could then be displayed for the user. Each new answer changes the survey results.

When you use a web-based search engine, the browser normally supplies the information you specify in an HTML form to the search engine with a GET request. The search engine performs the search, then returns the results to you as a web page. Such pages are sometimes cached by the browser in case you perform the same search again.

## 29.3 Multitier Application Architecture

Web apps are multitier applications (sometimes referred to as n-tier applications). Multitier applications divide functionality into separate tiers (i.e., logical groupings of functionality). Although tiers can be located on the same computer, the tiers of web apps often reside on separate computers. Figure 29.3 presents the basic structure of a three-tier web app.

![](img/009e962758dcc71dbc43a493362e6dc0_1278_0.png)

Fig. 29.3 | Three-tier architecture.

The information tier (also called the data tier or the bottom tier) maintains data pertaining to the application. This tier typically stores data in a relational database management system (RDBMS). We discussed RDBMSs in Chapter 28. For example, a retail store might have a database for storing product information, such as descriptions, prices and quantities in stock. The same database also might contain customer information, such as user names, billing addresses and credit card numbers. This tier can contain multiple databases, which together comprise the data needed for our application.

The middle tier implements business logic, controller logic and presentation logic to control interactions between the application’s clients and the application’s data. The middle tier acts as an intermediary between data in the information tier and the application’s clients. The middle-tier controller logic processes client requests (such as requests to view a product catalog) and retrieves data from the database. The middle-tier presentation logic then processes data from the information tier and presents the content to the client. Web apps typically present data to clients as HTML documents.

Business logic in the middle tier enforces business rules and ensures that data is reliable before the server application updates the database or presents the data to users. Business rules dictate how clients can and cannot access application data, and how applications process data. For example, a business rule in the middle tier of a retail store’s web app might ensure that all product quantities remain positive. A client request to set a negative quantity in the bottom tier’s product-information database would be rejected by the middle tier’s business logic.

The client tier, or top tier, is the application’s user interface, which gathers input and displays output. Users interact directly with the application through the user interface (typically viewed in a web browser), keyboard and mouse. In response to user actions (e.g., clicking a hyperlink), the client tier interacts with the middle tier to make requests and to retrieve data from the information tier. The client tier then displays the data retrieved from the middle tier to the user. The client tier never directly interacts with the information tier.

## 29.4 Your First JSF Web App

Let’s begin with a simple example. Figure 29.4 shows the output of our WebTime app. When you invoke this app from a web browser, the browser requests the app’s default JSF page. The web server receives this request and passes it to the JSF web-application framework for processing. This framework is available in any Java EE 6-compliant application server (such as the GlassFish application server used in this chapter) or any JavaServer
