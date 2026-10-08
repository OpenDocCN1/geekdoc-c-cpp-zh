Active Server Pages (ASP), which is also known as Classic ASP, is Microsoft’s answer to these requirements. Overall, ASP is not a programming language, but rather a programming framework. It's a special programming method embedded in HTML pages. During the processing of the ASP page, the web engine parses the content of the page. It displays the HTML code parts and runs the embedded ASP scripts. Finally, IIS sends the code from the HTML and ASP result to the client.

Following is an example:

```
<HTML>
<HEAD><TITLE>Visual Studio 2010 Welcome Page</TITLE></HEAD>
<BODY>
<% Response.Write("<h1>Hello Visual Studio 2010!</h1>") %>
</BODY>
</HTML>
```

The language of most ASP pages is JavaScript or VBScript, but other third-party active scripting languages have evolved as well (for example, PerScript).

# ENTER ASP.NET

ASP was a good solution for server-side active scripting, but it experiences a problem. The presentation and content are mixed together. In 1997, Microsoft began realizing how to solve this problem. The task of developing the new model was given to two young professionals, Mark Anders (a manager of IIS team) and Scott Guthrie (who joined Microsoft in 1997, and is currently the Corporate Vice President of .NET Developer Platform).

Guthrie offered the following description of the birth of ASP.NET:

> We actually started the ASP.NET project in late 1997 and early 1998. At the time, ASP was still relatively new, and we initially weren't sure whether there was anything left to do in the web. (Double we spent a lot of time talking with developers and customers using ASP, and quickly realized that there were a lot of things to resolve.

> Some specific issues/requests come up and again from customers — provide the ability to write much cleaner code that provided good code/content separation (rather than mixing code up in the HTML), provide the ability to write applications using a variety of coding languages (and not just VBScript and JavaScript), deliver a more robust execution environment (avoiding memory leaks and crashes that could bring down the server), provide a much cleaner configuration/code deployment model, deliver a built-in security architecture, enable built-in output caching support to improve scalability, and more.