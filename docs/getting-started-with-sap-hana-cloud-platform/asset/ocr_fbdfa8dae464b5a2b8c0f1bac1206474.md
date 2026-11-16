Once the application's deployed, you can play around with the reading list and test the application flow to see how the Servlet and JSP components interact with one another. We should also point out that you have the option of copying the URL from the embedded browser window in Eclipse during the course of your testing and pasting it into the address bar of your favorite browser (e.g., Google Chrome, Mozilla Firefox, etc.) so that you can better approximate the end user experience.

# 3.3 Working with EJBs

As we noted in Chapter 2, the Java EE 6 Web profile provides support for EJB development using session beans. This allows us to factor our business logic out of the presentation layer (i.e., Servlets and JSPs) and into a series of session beans. Although we could conceivably achieve the same designs using POJOs, there are several benefits to be gained by using EJBs, including built-in transaction management, security, pooling, and more. With that in mind, this section will demonstrate how to integrate EJBs into our Java-based web applications.

# 3.3.1 Refactoring for EJBs

To illustrate how to work with EJBs, we'll refactor the reading list application that we developed in Section 3.2 by moving all of the business logic from the Java Servlet tier into a session EJB. Because we don't have a persistence layer yet, we'll approximate this by defining our EJB as a stateless session EJB. That way, our EJB can keep track of the individual reading lists, and our Servlet/JSP layer can focus on rendering the UI content and controlling page flow.

To kick off the refactoring effort, we elected to create a brand new Dynamic Web project and then copy over all the resources from the original reading list application. With this new project in place, we're ready to proceed with the development of our new EJB component. The steps for creating the EJB are as follows:

+   1. Right-click on the main project node and select the New • OTHER... menu path, as shown in Figure 3.14.

+   2. In the wizard selection dialog box (Figure 3.15), expand the EJB folder and select the SESSION BEAN (EJB 3.x) entry. Click on the NEXT > button to proceed.