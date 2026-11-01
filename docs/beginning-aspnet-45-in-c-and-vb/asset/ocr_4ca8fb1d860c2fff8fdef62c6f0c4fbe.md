# Dynamic Data

The controls in this category are used in Dynamic Data websites. Dynamic Data sites enable you to quickly build a user interface to manage data in a database. These controls are not discussed further in this book. To learn more about them, check out Sams' ASP.NET Dynamic Data Unleashed, Oleg Sych and Randy Patterson, 2012 (ISBN: 978-0-672-33565-5).

# THE ASP.NET STATE ENGINE

In the previous chapter, you created a page with a TextBox and a Button control. In the Try It Out, you ran this page in the browser, typed some text, and clicked the button. The button caused a postback to the server, and when the page reloaded, the text was still present in the text box. You pretty much did the same thing with the Wizard control in this chapter, where the values from the text box and the drop-down list were maintained as well. If you're familiar with other web technologies like ASP or PHP, this probably surprised you. In those languages, you often need to write lots of code to make this happen. So why and how does this work automatically in ASP.NET?

The text in the text box is maintained by the ASP.NET state engine, a feature that is deeply integrated into the ASP.NET run time. It enables controls to maintain their state across postbacks, so their values and settings remain available after every postback of the page.

# What Is State and Why Is It Important?

To understand state, it's important to realize that, by design, HTTP—the protocol used to request and serve pages in a web browser—is stateless. What this means is that the web server does not keep track of requests that have been made from a specific browser. As far as the web server is concerned, each request you make to the server by browsing to a page and clicking links to other pages stands on its own. The web server has no recollection of pages you requested previously.

This poses some interesting problems. Consider, for example, a simple login page that enables you to log in to a website, like your favorite web mail program. You can see a sample of the login box in Figure 4-16.

![](bbox=[0.6, 0.72, 0.93, 0.86])

Now imagine that you try to log in with a correct username but with an incorrect password. The page will then inform you that your login attempt failed. Ideally, you would also want your username to be filled in for you automatically, and you'd want the Remember Me Next Time check box to retain its selection as well. That way, it's easy for the user to enter the correct password and click the Log In button again. This is just a trivial example, but it's easy to come up with many more scenarios where it's useful if controls are able to maintain their own state.

However, by default, a web page or a control cannot do this on its own. Because each request is a standalone request, the server won't fill in the text boxes again after a postback, but will simply