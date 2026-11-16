
![](img/cf7012644082c115a2181376d9b7486d_84_0.png)

Figure 3.8 Creating the JSP-Based View: Part 1

![](img/cf7012644082c115a2181376d9b7486d_84_1.png)

Figure 3.9 Creating the JSP-Based View: Part 2

As you can see in Listing 3.2, the form UI is implemented using some basic HTML5-compliant markup and a few well-placed JSTL scriptlet tags. These tags are used to simplify handling of the dynamic reading list data. Underneath the reading list, we've included an HTML form that allows users to add additional books to the list. As you might expect, this form is linked back to our ReadingListServlet to update the reading list.

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<jsp:useBean id="readingList" scope="session"
    class="java.util.ArrayList" />

<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="Content-Type"
        content="text/html; charset=UTF-8">
    <title>HCP Book : Chapter 3 : My HCP Reading List</title>
    <link href="css/style.css" rel="stylesheet">
</head>
<body>
    <h1>My HCP Reading List</h1>
    <table class="readingList">
        <tr>
            <th>Book Title</th>
        </tr>
        <c:forEach var="book" items="${readingList}">
            <c:forEach var="title" value="${book}">
                <td>${title}</td>
            </c:forEach>
        </c:forEach>
    </table>
    <section>
        <form method="post" action="ReadingListServlet">
            <label for="inpBook">
                Book: <input id="inpBook" name="book" />
            </label>&nbsp;
            <button type="submit">Add</button>
        </form>
    </section>
</body>
</html>
```

### Listing 3.2 Implementing the JSP-Based View Layer

## 3.2.4 Testing the Application Locally

With all of the code now in place, we're ready to test our application. Because we're dealing with a pure Java-based web application, we could technically test this application on most any Java web server. However, because the target run-time is ultimately SAP HCP, it makes sense to run our test using the SAP HCP local runtime that's bundled with the SAP HCP SDK. The steps required to test our application on this local runtime are as follows:

- 1. Create a new run configuration within Eclipse by right-clicking on the project folder and choosing the Run As > Run on Server menu option, as shown in Figure 3.10.

![](img/cf7012644082c115a2181376d9b7486d_86_0.png)

Figure 3.10 Testing the Reading List Application: Part 1

- 2. This will open up the Run On Server dialog box (Figure 3.11). Here, select the server instance that you want to run your application on. Because this is the first time you're running an application on the SAP HCP local runtime, choose the MANUALLY Define a New Server radio button option so that you can configure the SAP HCP local runtime as a server within Eclipse. This configuration amounts to the selection of the appropriate runtime environment from within the SAP server type selection list (Figure 3.11). Click on the Next > button to continue.

![](img/cf7012644082c115a2181376d9b7486d_87_0.png)

### Figure 3.11 Testing the Reading List Application: Part 2

- 3. On the next screen, select the target HTTP port for your new local server instance. Normally, you'll want to choose an available 8000 series port (e.g., 8080) on your local machine for this, so it's usually best to simply go with the default port selection proposed by Eclipse.

- 4. Finally, trigger the deployment/test by clicking on the Finish button. At this point, Eclipse will attempt to deploy your application onto the target SAP HCP local runtime instance. The SAP HCP local runtime environment will be started if it's not started already. Assuming the deployment is a success, the default index.jsp file will be loaded into an embedded browser window, as shown in Figure 3.13.

![](img/cf7012644082c115a2181376d9b7486d_88_0.png)

Figure 3.12 Testing the Reading List Application: Part 3

![](img/cf7012644082c115a2181376d9b7486d_88_1.png)

Figure 3.13 Testing the Reading List Application: Part 4

Once the application's deployed, you can play around with the reading list and test the application flow to see how the Servlet and JSP components interact with one another. We should also point out that you have the option of copying the URL from the embedded browser window in Eclipse during the course of your testing and pasting it into the address bar of your favorite browser (e.g., Google Chrome, Mozilla Firefox, etc.) so that you can better approximate the end user experience.

## 3.3 Working with EJBs

As we noted in Chapter 2, the Java EE 6 Web profile provides support for EJB development using session beans. This allows us to factor our business logic out of the presentation layer (i.e., Servlets and JSPs) and into a series of session beans. Although we could conceivably achieve the same designs using POJOs, there are several benefits to be gained by using EJBs, including built-in transaction management, security, pooling, and more. With that in mind, this section will demonstrate how to integrate EJBs into our Java-based web applications.

### 3.3.1 Refactoring for EJBs

To illustrate how to work with EJBs, we'll refactor the reading list application that we developed in Section 3.2 by moving all of the business logic from the Java Servlet tier into a session EJB. Because we don't have a persistence layer yet, we'll approximate this by defining our EJB as a stateless session EJB. That way, our EJB can keep track of the individual reading lists, and our Servlet/JSP layer can focus on rendering the UI content and controlling page flow.

To kick off the refactoring effort, we elected to create a brand new Dynamic Web project and then copy over all the resources from the original reading list application. With this new project in place, we're ready to proceed with the development of our new EJB component. The steps for creating the EJB are as follows:

- 1. Right-click on the main project node and select the New > OTHER... menu path, as shown in Figure 3.14.

- 2. In the wizard selection dialog box (Figure 3.15), expand the EJB folder and select the SESSION BEAN (EJB 3.x) entry. Click on the NEXT > button to proceed.

![](img/cf7012644082c115a2181376d9b7486d_90_0.png)

Figure 3.14: Creating an EJB in a Dynamic Web Project: Part 1

![](img/cf7012644082c115a2181376d9b7486d_90_1.png)

Figure 3.15: Creating an EJB in a Dynamic Web Project: Part 2

- 3. This will open the CREATE EJB 3.x SESSION BEAN dialog box (Figure 3.16). Within this screen, there are several important properties that you need to configure for your EJB:

  - The target JAVA PACKAGE and CLASS NAME.
  - Within the Java type list, you need to choose whether the session EJB will be STATEFUL or STATELESS. For the purposes of our example, we've chosen the STATELESS option, because we want our EJB to keep track of application state. Most of the time, though, we prefer to go with the default STATELESS option, because it's more efficient.
  - Because you want to incorporate EJB method calls into the Servlet/JSP tier, you need to configure a local business interface for the EJB. This is achieved by selecting the LOCAL checkbox in the CREATE BUSINESS INTERFACE section.

![](img/cf7012644082c115a2181376d9b7486d_91_0.png)

### Figure 3.16 Creating an EJB in a Dynamic Web Project: Part 3

- 4. Once you've confirmed your selections, click on the Finish button to go ahead and create the session bean.

After the wizard is completed, we can see that there are two new source files added to our project: one for the session bean itself and the other for the local business interface. In the next section, we'll learn how to add our business logic to these source files.

### 3.3.2 Implementing Business Logic in an EJB

To begin developing the business logic, we start with the local business interface. This interface will define the business methods exposed to the Servlet/JSP tier. For the purposes of our reading list application, we created the four methods shown in Listing 3.3. These methods will allow users to add and remove titles from the reading list, obtain a live copy of the reading list, and determine the total number of entries in the list.

```
@Local
public interface ReadingListManagerBeanLocal
{
    public void addTitle(String title);
    public boolean removeTitle(String title);
    public int getCount();
    public List<String> getReadingList();
}
```

### Listing 3.3 Defining the EJB's Local Business Interface

As you can see in Listing 3.3, the local business interface looks pretty much like any other Java interface. The only EJB-centric element is the @Local annotation, which allows the EJB container to identify the interface as a local business interface.

After you save your business interface, you'll notice that the session bean class has been flagged with a little red ERROR icon within Eclipse. Because our session bean implements the local business interface, the error is indicating that our session bean contains unimplemented methods. To fix this problem, simply click on the ERROR icon in the margin to the left of the class definition statement and choose the ADD UNIMPLEMENTED METHODS option, as shown in Figure 3.17. This will add empty versions of each of the business methods to our session bean.
