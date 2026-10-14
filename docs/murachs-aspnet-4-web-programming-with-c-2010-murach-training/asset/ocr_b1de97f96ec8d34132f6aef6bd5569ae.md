# A custom error page in a browser

![](bbox=[0.156, 0.104, 0.822, 0.416])

# Four ways to display a custom error page when an exception occurs

+   - Use try-catch statements to catch exceptions as they occur, then redirect or transfer to a custom error page.
+   - Use the Page_Error method in a code-behind file to catch unhandled exceptions at the page level, then redirect or transfer to a custom error page.
+   - Use the Application_Error method in the global.asax file to catch unhandled exceptions at the application level, then redirect or transfer to a custom error page.
+   - Use the customErrors element of the web.config file to specify custom error pages that are displayed for specific types of HTTP errors.

# Description

+   - If an unrecoverable error occurs, most applications display a custom error page to inform the user that a problem has occurred.
+   - Behind the scenes, the custom error page may also record the error in a log or send an email message to the application’s support staff to notify them of the error.
+   - Custom error pages often use an Exception object to display a detailed message that describes the error.