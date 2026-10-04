
## Types of Controls | 123

complexity, the server controls a little more time to process. However, on most websites you won't notice the difference. Only when you have a high-traffic website with lots of controls on the page do the HTML controls give you a slightly better performance and consume less memory on the server compared to the server controls.

In most scenarios, favor server controls over their HTML counterparts. Because server controls offer more functionality, they give you more flexibility in your pages, enabling you to create a better user experience. Also, the better design-time support makes it worth choosing these controls.

Choose the HTML controls if you're really sure you don't need the functionality that the server offers you.

The remainder of this section guides you through the other categories in the Toolbox.

## Data Controls

Data controls were introduced in ASP.NET 2.0, and offer an easy access to various data sources like databases, XML files, and objects. Instead of using lists of code to access the data source you had to do in earlier versions of ASP.NET, you simply point your data control to an appropriate data source, and the ASP.NET run time takes care of most of the difficult issues for you. You will learn a lot about these controls in Chapter 13 and onward.

## Validation Controls

Validation controls enable you to rapidly create Web Forms with validation rules that prohibit users from entering invalid data. For example, you can force users to enter values for required fields and check whether the entered data matches a specific format like a valid date or a number between 1 and 10. They even allow you to write custom code to create validation routines that are not covered by the standard controls. The beauty of the validation controls is that they can execute both on the client and the server, enabling you to create responsive and secure web applications. Chapter 9 digs deeper into these controls.

## Navigation Controls

The controls you find under the Navigation category of the Toolbox are used to let users find their way through your site. The Tree control provides a hierarchical description of data and can be used to show the structure of your site, giving easy access to all the pages in your site. The Menu control does a similar thing and provides options for horizontal and vertical fold-out menus.

The SitemapPath control creates a "breadcrumb trail" in your web pages that enables users to easily find their way in the hierarchy of your site.

You will see all of these controls in action in Chapter 7, which deals with navigation in websites exclusively.

## Login Controls

Just like the data and navigation controls, the login controls were introduced in ASP.NET 2.0 and are still strongly present in ASP.NET 4.5.1. With very little effort, login controls enable you to
create secure websites where users need to sign up and log in before they can access specific parts of the website (or the entire website). In addition, they provide the tools for users to change their password, or request a new password if they forget the old one, and enable you to display different data depending on the logged-in status and role of the user. Chapter 16 provides more details about the security features and login controls of ASP.NET.

## Ajax Extensions

The Ajax Extensions enable you to create flicker-free web applications that are able to retrieve data from the server from client-side JavaScript without a full postback. You can find the full details on them in Chapter 10.

## WebParts

ASP.NET WebParts are a set of controls that enables an end user of a web page to change the appearance and behavior of a website. These controls are outside the scope of this book.

## Dynamic Data

The controls in this category are used in Dynamic Data websites. Dynamic sites enable you to quickly build a user interface to manage data in a database. These controls are not discussed further in this book. To learn more about them, check out Sams' ASP.NET Dynamic Data Unleashed, Oleg Sych and Rand Patterson, 2012 (ISBN: 978-0-672-33565-5).

## THE ASP.NET STATE ENGINE

In the previous chapter, you created a page with a TextBox and a Button. In the Try Out, you ran in this browser, typed some text, and clicked the button. The button caused a postback to the server, and when the page reloaded, the text was still present in the text box. You pretty much did the same with the drop-down list in the Wizard control in that chapter, where the values from the text box and the drop-down list were maintained. If you're familiar with other technologies like ASP or PHP, this probably surprised you. In those languages, you often need to write lines of code to make this happen. Why and how does this work automatically in ASP.NET?

The text in the text box is maintained by the ASP.NET state engine, a feature that is deeply integrated into the ASP.NET run time. It enables controls to maintain their state across postbacks, so their values and settings remain available after every postback of the page.

## What Is State and Why Is It Important?

To understand state, it's important to realize that by design, HTTP — the protocol used to request and serve pages in a web browser — is stateless. This means that the web server does not keep track of requests that have been made from a specific browser. As far as the web server is concerned, each request you make to the server by browsing to a page and clicking links to other pages stands on its own. The web server has no recollection of pages you requested previously.

## The ASP.NET State Engine

This poses some interesting problems. Consider, for an example a login page that enables you to log in to a website, like your favorite mail program. You can see a sample of the login box in Figure 4-16.

Now imagine you try to log in with a correct username but an incorrect password. The page will tell you that your login attempt failed. Ideally, you also want your username to be filled in automatically, and you'd want the Remember Me Next Time checkbox to retain its selection as well. That is, it's easy for the user to enter the correct password and click Log In button. This is just a trivial example, but with many more scenarios where it's useful for controls to maintain their state.

![](img/9e033e3b9560597824f8b22941d6d8bb_162_0.png)

However, by default, a web page or a control cannot do this on its own. Because each request is a standalone request, the server won't fill in the text boxes again after a postback. In other technologies, like classic ASP or PHP, you could work around this by manually writing code that prepopulates controls after a postback. Fortunately, ASP.NET makes this much easier for you by integrating this functionality into the ASP.NET framework.

## How the State Engine Works

The state in ASP.NET is capable of storing state for many controls. It cannot store only for input controls like a TextBox and a Checkbox, but for other controls like a Label and a Calendar. This is best demonstrated by a demo. The following exercise shows how to create a page with controls that are capable of maintaining their state. The sections that then explain how ASP.NET is able to do this.

> TRY OUT Examining the ASP.NET State Engine

In this exercise you add Label, Button, TextBox, and Calendar controls to the page. These controls are used to demonstrate some of the inner workings of ASP.NET, including postbacks and the way ASP.NET maintains state.

- 1. Under the demos folder, create a new page called State.aspx. Make sure it uses Code Behind, and do not forget to choose your preferred programming language.
- 2. Switch the page to Design View, click the dashed <div> to put the focus on it, and then choose Table > Insert Table from the menu. Set Rows to 3 and Columns to 2 and click OK to insert a table with three rows and two columns.
- 3. In the first cell of the first row, drag a Label control from the Toolbox. In the first cell of the second row, drag a Calendar control.
- 4. Note that as you drop the Calendar control in the cell, its Smart Tasks panel pops up as shown in Figure 4-17.

In the case of the Calendar control, you only get one option on this panel, Auto Format, which enables you to change the appearance of the calendar. Click the link, choose from one of the predefined schemes, like Simple, and click OK.
