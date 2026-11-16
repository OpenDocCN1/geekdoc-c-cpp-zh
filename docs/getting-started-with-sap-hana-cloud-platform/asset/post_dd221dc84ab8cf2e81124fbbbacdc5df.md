
the left-hand side of the group editor page (Figure 8.7). From here, you can add new roles to the group by clicking on the Assign button. This triggers a similar popup window to the one shown in Figure 8.6 for user role assignments.

After a group is defined, you can begin assigning users in the user assignment panel on the right-hand side of the Groups tab page (see Figure 8.7) or from the Users tab page shown in Figure 8.6. Both approaches get you to the same place, so which path you take is a matter of preference.

Even though groups make it easier to perform role assignments in bulk, there's no getting around the fact that such assignments still require a lot of administrative work whenever you're dealing with a large user base. With that in mind, in Section 8.5 we'll revisit the group assignment process and see how SAML can be used to automate group assignments.

## 8.4 Implementing Programmatic Security in Java

In the previous section, we demonstrated several techniques for declaratively specifying security constraints. Although these methods are effective for defining basic security constraints, they're not without their limitations. Indeed, if you want to implement conditional security logic and the like, then you're going to have to get your hands dirty with some custom Java code. In this section, we'll show you how to do just that.

### 8.4.1 Checking Authorizations Programmatically

In Section 8.3.2, you learned how to declaratively define security constraints that prevent unauthorized users from browsing to selected web resources. Although such a clear-cut approach to security is certainly desirable, there will be times when you need to provide users with conditional access to a web resource.

For example, imagine that you're building an employee directory application that allows employees within a company to look up information about their fellow employees. Within this application, suppose that there's an employee details page (perhaps written as a JSP) that displays basic employee contact information as well as more sensitive information such as the employee's personal contact number, emergency contact, and so forth. Although every employee in the company should be able to access basic contact information, you need to restrict access to sensitive information to selected authorized users, such as the employee's HR manager.

To implement something like this using the declarative approach, you would have to end up creating multiple pages: one for end users and one for managers. As you can imagine, this sort of approach can become quite tedious from a maintenance perspective.

A more economical approach would be to create a single page and conditionally restrict access to particular content sections based on a user's role assignments. With Servlets/JSPs, you can implement such conditional logic using the Boolean `isUserInRole()` method of the `javax.servlet.http.HttpServletRequest` interface. This approach is demonstrated in the JSP code excerpt contained in Listing 8.3. Here, the `<div>` content contained within the JSP `<%= %>` scriptlet tags is only displayed if the user is mapped to the manager role.

```
<%@ page language="java"...%>
<!DOCTYPE HTML>
<html>
<body>
...
<div id="BasicData">...</div>
<% if (request.isUserInRole("manager")) { %>
<div id="PersonalData">...</div>
<% } %>
</body>
</html>
```

### Listing 8.3 Programmatically Checking User Role Assignments

The code excerpt contained in Listing 8.4 shows how the same `isUserInRole()` method is used within a Java Servlet. Here, the method allows you to implement intelligent routing in a classic model-view-controller (MVC) architecture in which the Servlet plays the role of controller and JSP pages provide the view layer.

```
public class RoutingServlet extends HttpServlet
{
    protected void doGet(HttpServletRequest request,
    HttpServletResponse response)
    throws ServletException, IOException
    {
    RequestDispatcher rd = null;
    if (request.isUserInRole("manager"))
    {
    rd = request.getRequestDispatcher("ManagerLaunchpad.jsp");
    rd.forward(request, response);
    }
    else
    {
    rd = request.getRequestDispatcher("EmployeeLaunchpad.jsp");
    rd.forward(request, response);
    }
    }
}
```

### Listing 8.4 Using Programmatic Authorization Checks

### 8.4.2 Working with the User Management API

By default, the Java Servlet API provides two methods that you can use to determine the name of the user logged onto the application. Both of these methods are contained within the javax.servlet.http.HttpServletRequest interface, and they are called getRemoteUser() and getUserPrincipal().

Although it's useful to be able to determine the user name of a logged-on user, there are typically other things that you'd also like to know about the user, including the following:

- Basic attributes of the user, such as the user's first and last name, email address, and so on
- The user's locale and preferences (e.g., country of origin, language spoken, etc.)
- The set of all roles and groups the user is assigned to
- The validity date of the user (if applicable)

Although the availability of much of this data is dependent on the capabilities of the underlying IdP, you can get your hands on the data that is available by using the SAP HCP User Management API contained within the com.sap.security.um.* package hierarchy.

> Note
> You can find a complete overview of the API functions available in the User Management API online at https://help.hana.ondemand.com/javadoc/index.html.

The code excerpt contained in Listing 8.5 demonstrates how to interface with the User Management API. Here, API access is provided through the com.sap.security.um.user.UserProvider interface, which can be used to look up information about a user. It should be noted that the user you query information about doesn't necessarily have to be the currently logged-on user; you could look up information about other users as well. In any case, once you have your hands on a com.sap.security.um.user.User instance, you can utilize its various getter methods to find out as much information about a user as is provided by the IdP.

```
import com.sap.security.um.user.User;
import com.sap.security.um.user.UserProvider;
import com.sap.security.um.service.UserManagementAccessor;
...
try {
    // Assumption: Only query the attributes for a logged-on user:
    if (request.getUserPrincipal() != null) {
        // Use the UserManagementAccessor factory to obtain an
        // instance of the UserProvider:
        UserProvider userProvider =
            UserManagementAccessor.getUserProvider();
    }
    // Then, lookup the User record:
    User user =
        userProvider.getUser(request.getUserPrincipal().getName());
    // Enumerate the attributes assigned to the user:
    for (String attr : user.listAttributes()) {
        response.getWriter().println(
            attr + " : " + user.getAttribute(attr));
    }
    // List the user's role assignments:
    for (String role : user.getRoles()) {
        response.getWriter().println(role);
    }
}
catch (Exception ex) { }
```

### Listing 8.5 Working with the User Management API

Although the code excerpt contained in Listing 8.5 showed how to obtain a UserProvider instance via the UserManagementAccessor factory, there are actually a couple of other ways you can get your hands on this instance. One approach is to declare the UserProvider as a resource reference in the web.xml deployment descriptor, as shown in Listing 8.6. With the resource reference defined, you can look up the UserProvider in your application using a JNDI lookup.

```
<web-app>
...
<resource-ref>
<res-ref-name>user/Provider</res-ref-name>
<res-type>com.sap.security.um.user.UserProvider</res-type>
</resource-ref>
</web-app>
```

### Listing 8.6 Declaring the User Provider as a Resource Reference

Alternatively, if the SAP HCP instance you're working with is based on the Java EE 6 Web profile, then you can inject the UserProvider instance using the @Resource annotation, as shown in Listing 8.7.

```
@Resource
private UserProvider userProvider;
```

### Listing 8.7 Injecting the UserProvider Instance

In addition to providing information about specific users, the UserProvider interface also contains a powerful search method called searchUser(), which can be used to search for users based on various types of search criteria. This feature can come in handy whenever you want to identify classes of users, for instance.

### 8.4.3 Working with the Authentication API

In Section 8.2.2, we mentioned that most Java EE server vendors prefer to externalize authentication and authorization handling logic to a series of modules built using JAAS. Although such details are typically abstracted from developers, this doesn't necessarily mean that developers can't get their hands on these modules to interface with this functionality directly.

Within SAP HCP, access to JAAS modules and callback handlers is provided in the form of the Authentication API contained in the com.sap.security.auth.login package. Using this API, you can programmatically trigger a user login or logout as needed.

The code excerpt contained in Listing 8.8 demonstrates how you can use the Authentication API to dynamically trigger a form-based login in situations in which the user hasn't authenticated already. Here, the call to the javax.security.auth.login.LoginContext interface's login() method does the trick, temporarily rerouting the user to a form logon page like the one illustrated in Figure 8.3. After the user authenticates, the program picks up where it left off with the logged-on user information in tow.
