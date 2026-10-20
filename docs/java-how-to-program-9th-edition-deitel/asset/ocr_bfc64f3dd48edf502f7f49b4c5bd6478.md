# Self-Review Exercises

29.1 State whether each of the following is true or false. If false, explain why.

+   a) A URL contains information that directs a browser to the resource that the user wishes to access.
+   b) Host names are translated into IP addresses by web servers.
+   c) The path in a URL typically specifies a resource’s exact location on the server.
+   d) GET requests and POST requests can both be used to send form data to a web server.
+   e) Browsers typically cache the server’s response to a POST request.
+   f) A tag library defines a set of elements that can be inserted into the XHTML markup.
+   g) You must create and manage the JavaBean objects that are used in your JSF web applications.
+   h) When the Faces servlet encounters an EL expression that accesses a bean property, it automatically invokes the property’s set or get method based on the context in which the property is used.
+   i) An h:panelGrid element organizes elements in an XHTML table.
+   j) An h:selectOneMenu element is typically rendered in a web page as a set of radio buttons.
+   k) The messages specified by an element’s requiredMessage and validatorMessage attributes are displayed in an associated h:message element when validation fails.
+   l) The HTTP protocol provides information that enables web servers to maintain state information regarding particular clients.
+   m) The ui:repeat element inserts its nested element(s) once for each element in a collection. The collection can be any IEnumerable type.

29.2 Fill in the blanks in each of the following statements:

+   a) Java multitier applications are typically implemented using the features of ________.
+   b) Computers that run ________ software make resources available, such as web pages, images, PDF documents and even objects that perform complex tasks.
+   c) The JSF web-application framework’s ________ processes each requested JSF page.
+   d) A(n) ________ exposes its data as read/write, read-only or write-only properties.
+   e) The ________ annotation indicates that the JSF framework should create and manage instances of the class.
+   f) A(n) ________ element contains the components with which a user interacts to provide data, such as registration or login information, to a JSF app.
+   g) A(n) ________ element triggers an action when clicked.
+   h) A(n) ________ validator determines whether a field contains an acceptable number of characters.
+   i) A(n) ________ validator determines whether a field contains a string that matches a specified regular expression pattern.
+   j) In a(n) ________, the browser re-requests the page and sends the values of the form’s fields to the server for processing.
+   k) A(n) ________ bean is created when a session begins and exists throughout the entire session.

# Answers to Self-Review Exercises

29.1 a) True. b) False. Host names are translated into IP addresses by DNS servers. c) False. The server translates a virtual directory into a real location, thus hiding a resource’s true location. d) True. e) False. Browsers typically do not cache the server’s response to a POST request, because the next POST might not return the same result. f) True. g) False. The JSF framework creates and manages objects of your JavaBean classes for you. h) True. i) True. j) False. An h:selectOneRadio ele-