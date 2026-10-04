# 414 Building Secure Web Forms Applications

![](bbox=[0.142, 0.126, 0.218, 0.183])

The easiest way to prevent SQL Injection is to never use string concatenation- to generate SQL. Use a stored procedure and SQL parameters. You can read more about that in Chapter 2 of this minibook.

# Script exploits

A script exploit is a security flaw that takes advantage of the JavaScript engine in the user's web browser. Script exploits take advantage of one of the most common features of public Web Forms applications — enabling interaction among users. For instance, a Web Forms application may enable a user to post a comment that others of the site can view, or it may allow a user to fill out an online profile.

If a malicious user were to put some script code in his profile or comment, hacker could take over the browser of the next user who comes to the site. Several outcomes are possible, and none of them are good.

For instance, the cookies collection is available to JavaScript when a user comes to your site. A malicious user would put some script code in his profile that copy the code for your site to a remote server. This could give the malicious user access to the current user's session because the session identifier is stored as a cookie. The malicious user would then be able to spoof the current user's identity.

Fortunately, ASP.NET prevents users from typing most script code into a form field and posting it to the server. Try it with a basic Web Forms project by following these steps (you see the error shown in Figure 1-3):

+   1. Create a new Web Forms project.
2. Add a text box and a button to the default page.
3. Run the project.
4. Type <script-msgbox()</script> into the text box.
5. Click the button.

![](bbox=[0.142, 0.725, 0.218, 0.793])

Additionally, you can use the Server.HtmlEncode method to encode anything that the Web Forms application sends to the screen — this will make script code appear in real text rather than in HTML.

# Best practices for securing Web Forms applications

Aside from making sure that your Web Forms application will prevent SQL injection attacks and script exploits, you should keep in mind some good practices for securing your web applications.