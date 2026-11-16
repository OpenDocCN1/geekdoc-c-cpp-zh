
## 3.2 Creating Java Web Applications

At the end of the day, any Java-based SAP HCP application that we develop must be deployed as a Java Web Archive (or WAR) file. Inside this WAR file, we can include a wide variety of resources, including Java class files, Servlets/JSPs, and static HTML artifacts. Although we’ll be looking at many of these different resource types as we go along, we thought it appropriate to start things off with a very simple Java web application based on Servlets and JSPs.

To guide our demonstration, we’ll be developing a simple application via which users can maintain a reading list. Here, we’ll create a simple JSP form to display the reading list and add additional titles. On the backend, we’ll develop a faceless, Servlet-based controller class to collect and keep track of the reading list entries. This application, though trivial, will provide us with an opportunity to learn how to work with the Eclipse IDE and observe how Java web applications are packaged. Plus, it will give us a chance to play around a bit with the local runtime environment packaged with the SAP HCP SDK. Without further ado, let’s get started.

### 3.2.1 Creating a Dynamic Web Project in Eclipse

To get things started, we need to open up the Eclipse IDE and create a new Dynamic Web project. This project type is the default project type for building Java-based web applications and is included as part of the Eclipse Java EE development tools. To create a new Dynamic Web project, we must perform the following steps:

- 1. Open Eclipse, and switch to the Java EE perspective. If you’ve never accessed this perspective before, you can do so by choosing Window • Open Perspective • Other... in the top-level menu bar and selecting the Java EE list option.

- 2. Once the Java EE perspective is opened, create a new Dynamic Web project by selecting the FILE • NEW • DYNAMIC WEB PROJECT menu option, as shown in Figure 3.1.

![](img/cf7012644082c115a2181376d9b7486d_77_0.png)

Figure 3.1 Creating a Dynamic Web Project in Eclipse: Part 1

- 3. This will open the NEW DYNAMIC WEB PROJECT wizard, as shown in Figure 3.2. In the first step, specify the basic coordinates for the project, including the following:

  - The project name (e.g., EXAMPLE03_01).

  - The location where you want to store the project artifacts within the local file system. Normally, it makes sense to keep the Use DEFAULT LOCATION checkbox selected, as this will ensure that the project artifacts get stored in the default Eclipse workspace.

  - The target runtime environment (i.e., the local runtime environment you set up whenever you downloaded the SAP HCP SDK).

  - The version of the Dynamic Web Module you wish to create. Here, the numbers in the Dynamic Web Module Version list correspond with versions of the Java Servlet API. Unless you have a compelling reason to configure it otherwise, we strongly recommend that you choose version 3.0, as illustrated in Figure 3.2.

![](img/cf7012644082c115a2181376d9b7486d_78_0.png)

Figure 3.2 Creating a Dynamic Web Project in Eclipse: Part 2

- 4. After the basic project coordinates are set, proceed forward through the project creation wizard by clicking on the **Next >** button. For the most part, you can accept the proposed defaults at the intermediate steps. However, at the **Web Module** step, we recommend that you select the **GENERATE WEB.XML DEPLOYMENT DESCRIPTOR** checkbox, as this will automatically create the web project's web.xml file and ensure that it's linked up with the Eclipse Java EE toolset.

- 5. Finally, once all of the settings are configured, click on **Finish** to confirm your selections and create the project. At this point, Eclipse will create the project folder structure and generate relevant project files, such as the aforementioned web.xml file.

Figure 3.3 shows what the project looks like in the Eclipse Project Explorer view once it's been created. Here, we can see that the project creation wizard has furnished us with everything we need to get started with development, including the following:

- 1. Underneath the Java Resources node, you can see that a folder called src has been created to store our Java source code files.

- 2. The project also contains references to all of the libraries needed to build Java-based web applications. This includes the basic Java SE libraries, Java EE libraries, and SAP HCP-specific libraries.

- 3. A WebContent folder mirrors the structure of the WAR file that will be used to deploy our web folder. As you can see, this includes the aforementioned prebuilt web.xml deployment descriptor.

![](img/cf7012644082c115a2181376d9b7486d_79_0.png)

Figure 3.3 Basic Structure of a Dynamic Web Project in Eclipse

The last step in the project setup process involves the creation of a Java package to store our Java source files. To create a new package, simply right-click on the src folder and select the New • PACKAGE menu option, as shown in Figure 3.4. Then, in the New JAVA PACKAGE dialog box, specify the package name using the familiar Java package naming convention based on reverse Internet domain names (see Figure 3.5).

![](img/cf7012644082c115a2181376d9b7486d_80_0.png)

Figure 3.4 Creating a Java Package: Part 1

![](img/cf7012644082c115a2181376d9b7486d_80_1.png)

Figure 3.5 Creating a Java Package: Part 2

### 3.2.2 Building the Servlet-Based Controller

With our Dynamic Web project now in place, we're ready to begin developing the actual application artifacts. In keeping with the traditional model-view-controller (MVC) paradigm, we'll start our development from the bottom up with the creation of a hybrid model-controller layer. As mentioned earlier, we'll implement this layer using a faceless Java Servlet class.

To create the Servlet, right-click on the development package created in Section 3.2.1 and choose the NEW > SERVLET menu option, as shown in Figure 3.6. Then, in the CREATE SERVLET dialog box (Figure 3.7), specify the Servlet class name (ReadingListServlet), and click on the Finish button to confirm your selection and create the new Servlet class.

![](img/cf7012644082c115a2181376d9b7486d_81_0.png)

Figure 3.6 Creating the Servlet Controller Class: Part 1

![](img/cf7012644082c115a2181376d9b7486d_82_0.png)

Figure 3.7 Creating the Servlet Controller Class: Part 2

After the Servlet class is created, we'll want to plug in our custom application logic inside the doPost() method, as shown in Listing 3.1. Here, the logic is pretty straightforward:

- 1. First, create a variable of type java.util.List called readingList. This variable will be used to store the book entries in the user's reading list. Because our trivial application is not backed by a database, we'll simply store this transient collection inside the user's session context. Note that once this list instance is created, we'll simply fetch it from the session context in subsequent calls to simulate access to a persistence store.

- 2. Next, retrieve the name of the book the user wants to add to the list by using the getParameter() method of the HttpServletRequest variable passed via the Servlet container. Here, we're retrieving the book's name via an HTTP request parameter called book.

- 3. Then, add the book to the reading list by calling the add() method of the readingList list object. While we're at it, we also update the session context with another attribute called itemCount that allows us to keep track of the number of books in the reading list.

- 4. Finally, use the javax.servlet.RequestDispatcher class to (re)direct the user back to the JSP form so that he or she can browse and/or make further updates to the reading list.

```
public class ReadingListServlet extends HttpServlet
{
    ...
    protected void doPost(HttpServletRequest request,
            HttpServletResponse response)
            throws ServletException, IOException
    {
        // Retrieve the current list from the user's session:
        List<String> readingList = null;
        HttpSession session = request.getSession();
        Object o = session.getAttribute("readingList");
        if (o == null)
        {
            readingList = new ArrayList<String>();
            session.setAttribute("readingList", readingList);
        }
        else
        {
            readingList = (List<String>) o;
        }
        // Add the selected item to the list:
        String book = request.getParameter("book");
        if (book != null)
            readingList.add(book);
        // Also keep track of the number of items in the list:
        session.setAttribute("itemCount", readingList.size());
        // Reroute the user back to the main reading list form:
        RequestDispatcher rd =
                request.getRequestDispatcher("index.jsp");
        rd.forward(request, response);
    }
}
```

Listing 3.1 Implementing the Servlet Controller Logic

### 3.2.3 Creating the View Layer Using JSPs

As we noted earlier, the view layer for our application is implemented using JSPs. To create the JSP form, perform the following steps:

- 1. Right-click on the WebContent folder and choose the New • JSP File menu option, as shown in Figure 3.8.

- 2. In the New JSP File dialog box (Figure 3.9), enter the JSP file name (e.g., index.jsp), and click on FINISH.
