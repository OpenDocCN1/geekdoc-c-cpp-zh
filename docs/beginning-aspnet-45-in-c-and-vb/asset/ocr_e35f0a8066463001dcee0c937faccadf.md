library—while still present in ASP.NET 4.5—is no longer the recommended solution. Instead, you're encouraged to use jQuery, which is discussed in detail in the next chapter.

The server-side part of Microsoft ASP.NET AJAX gives you a lot more than flicker-free postbacks. In addition to the controls that make flicker-free pages possible, Microsoft ASP.NET AJAX gives you a few more server controls to create rich, interactive, and responsive user interfaces.

# THE CORRECT SPELLING OF AJAX

> You'll come across two different spellings of Ajax: using Pascal casing, or in all caps. I'll use the term Ajax when referring to the general concept, and I'll use ASP.NET AJAX when specifically referring to Microsoft's Ajax framework.

By the end of the chapter, you should have a good understanding of the various server controls that the ASP.NET AJAX Framework has to offer. You will also have a basic understanding of creating WCF Services and page methods using ASP.NET and how you can call them from client-side JavaScript code.

# INTRODUCING AJAX

In the first chapter of this book you learned how browsers interact with the server. The browser makes a request for a page using GET or POST, as you've seen in Chapter 4 and Chapter 9. The server processes that page and sends back the resulting HTML. The browser then parses that HTML and renders the page to the user, optionally downloading any external resources like images, script files, and cascading style sheets (CSS). When a user interacts with the page (for example, by clicking a button to submit a filled-in contact form) the page is posted back to the server, after which the entire page is loaded in the browser again. The left-hand side of Figure 10-1 shows a visual representation of this process.

![](bbox=[0.12, 0.72, 0.88, 0.98])