# ## 3.2 Creating Java Web Applications

At the end of the day, any Java-based SAP HCP application that we develop must be deployed as a Java Web Archive (or WAR) file. Inside this WAR file, we can include a wide variety of resources, including Java class files, Servlets/JSPs, and static HTML artifacts. Although we’ll be looking at many of these different resource types as we go along, we thought it appropriate to start things off with a very simple Java web application based on Servlets and JSPs.

To guide our demonstration, we’ll be developing a simple application via which users can maintain a reading list. Here, we’ll create a simple JSP form to display the reading list and add additional titles. On the backend, we’ll develop a faceless, Servlet-based controller class to collect and keep track of the reading list entries. This application, though trivial, will provide us with an opportunity to learn how to work with the Eclipse IDE and observe how Java web applications are packaged. Plus, it will give us a chance to play around a bit with the local runtime environment packaged with the SAP HCP SDK. Without further ado, let’s get started.

# ### 3.2.1 Creating a Dynamic Web Project in Eclipse

To get things started, we need to open up the Eclipse IDE and create a new Dynamic Web project. This project type is the default project type for building Java-based web applications and is included as part of the Eclipse Java EE development tools. To create a new Dynamic Web project, we must perform the following steps:

+   1. Open Eclipse, and switch to the Java EE perspective. If you’ve never accessed this perspective before, you can do so by choosing Window • Open Perspective • Other... in the top-level menu bar and selecting the Java EE list option.

+   2. Once the Java EE perspective is opened, create a new Dynamic Web project by selecting the FILE • NEW • DYNAMIC WEB PROJECT menu option, as shown in Figure 3.1.