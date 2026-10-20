+   c) is a technology for locating application components (such as databases) in a distributed application.
+   d) A(n) ________ enables a web application to obtain a Connection to a database.
+   e) The annotation ________ can be used to inject a DataSource object into a managed bean.
+   f) A(n) ________ element displays a collection of objects in tabular format.
+   g) An h:commandButton’s ________ attribute can specify the name of another page in the web app that should be returned to the client.
+   h) To specify headers or footers for the columns in h:dataTables, use ________ elements nested with their name attributes set to ________ and ________, respectively.
+   i) ________ separates the user interaction portion of an application from its server interaction, enabling both to proceed asynchronously in parallel.
+   j) ________ help make web applications more responsive, making them feel more like desktop applications.
+   k) The f:ajax element’s ________ attribute specifies a space-separated list of element ids—the values of these elements are submitted as part of the Ajax request.
+   l) The f:ajax element’s ________ attribute specifies a space-separated list of element ids for the elements that should be updated via partial page updates.

# Answers to Self-Review Exercise

30.1 a) Asynchronous JavaScript and XML. b) connection pool. c) JNDI (Java Naming and Directory Interface). d) DataSource. e) @Resource. f) h:dataTable. g) action. h) f:facet, "header", "footer". i) Ajax. j) partial page updates. k) execute. l) render.

# Exercises

30.2 (Guestbook Application) Create a JSF web app that allows users to sign and view a guestbook. Use the Guestbook database to store guestbook entries. [Note: A SQL script to create the Guestbook database is provided in the examples directory for this chapter.] The Guestbook database has a single table, Messages, which has four columns: Date, Name, Email and Message. The database already contains a few sample entries. Using the AddressBook app in Section 30.2 as your guide, create two Facelets pages and a managed bean. The index.xhtml page should show the Guestbook entries in tabular format and should provide a button to add an entry to the Guestbook. When the user clicks this button, display an addentry.xhtml page. Provide h:inputText elements for the user’s name and email address, an h:inputTextarea for the message and a Sign Guestbook button to submit the form. When the form is submitted, you should store in the Guestbook database a new entry containing the user’s input and the date of the entry.

30.3 (AddressBook Application Modification: Ajax) Combine the two Facelets pages of the AddressBook application (Section 30.2) into a single page. Use Ajax capabilities to submit the new address book entry and to perform a partial page update that rerenders h:dataTable with the updated list of addresses.

30.4 (AddressBook Application Modification) Modify your solution to Exercise 30.3 to add a search capability that allows the user to search by last name. When the user presses the Search button, use Ajax to submit the search key and perform a partial page update that displays only the matching addresses in the h:dataTable.