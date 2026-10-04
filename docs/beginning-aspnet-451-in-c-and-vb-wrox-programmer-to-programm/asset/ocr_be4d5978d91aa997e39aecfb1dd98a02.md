# Types of Controls | 123

complexity, the server controls a little more time to process. However, on most websites you won't notice the difference. Only when you have a high-traffic website with lots of controls on the page do the HTML controls give you a slightly better performance and consume less memory on the server compared to the server controls.

In most scenarios, favor server controls over their HTML counterparts. Because server controls offer more functionality, they give you more flexibility in your pages, enabling you to create a better user experience. Also, the better design-time support makes it worth choosing these controls.

Choose the HTML controls if you're really sure you don't need the functionality that the server offers you.

The remainder of this section guides you through the other categories in the Toolbox.

# Data Controls

Data controls were introduced in ASP.NET 2.0, and offer an easy access to various data sources like databases, XML files, and objects. Instead of using lists of code to access the data source you had to do in earlier versions of ASP.NET, you simply point your data control to an appropriate data source, and the ASP.NET run time takes care of most of the difficult issues for you. You will learn a lot about these controls in Chapter 13 and onward.

# Validation Controls

Validation controls enable you to rapidly create Web Forms with validation rules that prohibit users from entering invalid data. For example, you can force users to enter values for required fields and check whether the entered data matches a specific format like a valid date or a number between 1 and 10. They even allow you to write custom code to create validation routines that are not covered by the standard controls. The beauty of the validation controls is that they can execute both on the client and the server, enabling you to create responsive and secure web applications. Chapter 9 digs deeper into these controls.

# Navigation Controls

The controls you find under the Navigation category of the Toolbox are used to let users find their way through your site. The Tree control provides a hierarchical description of data and can be used to show the structure of your site, giving easy access to all the pages in your site. The Menu control does a similar thing and provides options for horizontal and vertical fold-out menus.

The SitemapPath control creates a "breadcrumb trail" in your web pages that enables users to easily find their way in the hierarchy of your site.

You will see all of these controls in action in Chapter 7, which deals with navigation in websites exclusively.

# Login Controls

Just like the data and navigation controls, the login controls were introduced in ASP.NET 2.0 and are still strongly present in ASP.NET 4.5.1. With very little effort, login controls enable you to